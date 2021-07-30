<html>

<head>
  <title>Tanserver API tester</title>
  <style>
    input {
      border: 1px solid #ccc;
      padding: 7px 0px;
      border-radius: 3px;
      padding-left: 5px;
      -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075);
      box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075);
      -webkit-transition: border-color ease-in-out .15s, -webkit-box-shadow ease-in-out .15s;
      -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
      transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s
    }

    input:focus {
      border-color: #e63b07;
      outline: 0;
      -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075), 0 0 8px #e63b07;
      box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075), 0 0 8px #e63b07
    }

    textarea {
      border: 1px solid #ccc;
      padding: 7px 0px;
      border-radius: 3px;
      padding-left: 5px;
      -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075);
      box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075);
      -webkit-transition: border-color ease-in-out .15s, -webkit-box-shadow ease-in-out .15s;
      -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
      transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s
    }

    textarea:focus {
      border-color: #e63b07;
      outline: 0;
      -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075), 0 0 8px #e63b07;
      box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075), 0 0 8px #e63b07
    }

    button {
      width: 200px;
      padding: 8px;
      background-color: #e63b07;
      border-color: #e63b07;
      color: #fff;
      -moz-border-radius: 10px;
      -webkit-border-radius: 10px;
      border-radius: 10px;
      -khtml-border-radius: 10px;
      text-align: center;
      vertical-align: middle;
      border: 1px solid transparent;
      font-weight: 900;
      font-size: 125%
    }
  </style>
</head>

<body>
  <script>
    /**
     * @param {String}  host Hostname of tanserver
     * @param {Integer} port Port of tanserver 
     */
    function Tanserver(host, port) {
      let worker;
      let _this = this;

      /**
       * @param  {Function} func Function that must run in background thread
       * @return {Worker}        Return a Worker instance executing func
       */
      let createWorker = (func) => {
        var blob = new Blob(['self.onmessage = ', func.toString()],
          { type: 'text/javascript' });

        return new Worker(URL.createObjectURL(blob));
      }

      /* Contains all worker code.  */
      let WorkerActions = async (e) => {

        /**
         * @param  {String} userApi    API name
         * @param  {String} jsonString Parameter of API as json 
         * @return {String} return header {"user_api":"...","json_length":"..."}\r\n
         */
        let makeHeader = (userApi, jsonLength) => {
          return `{"user_api":"${userApi}","json_length":${jsonLength}}\r\n`;
        }

        /**
         * @param  {String} userApi    API name
         * @param  {String} jsonString Parameter of API as json 
         * @return {String} return packet using custom protocol
         */
        let makePacket = (userApi, jsonString) => {
          return makeHeader(userApi, jsonString.length) + jsonString;
        }

        if (e.data.action == "run") {
          var ws = new WebSocket(`wss://${e.data.host}:${e.data.port}`);

          ws.onopen = function () {
            ws.send(makePacket(e.data.userApi, e.data.jsonString));
          }

          ws.onmessage = function (e) {
            ws.close();

            self.postMessage({
              'error': null,
              'jsonString': e.data.toString()
            });
          }

          ws.onclose = function (e) {

            /* 1000: Normal closure  */
            if (e.code != 1000) {
              self.postMessage({
                'error': "Network Error",
                'jsonString': null
              });
            }
          }
        }
      }

      /**
       * @param {String}   userApi                   API name
       * @param {String}   jsonString                Parameter of API as json  
       * @param {Function} completion(jsonData, err) Function executed if json is obtained successfully, it take 'value' as parameter that will contain the response from tanserver
       */
      _this.getJSON = (userApi, jsonString, completion) => {

        if (typeof (worker) == "undefined") {
          worker = createWorker(WorkerActions);
        }

        /* Handle answer from worker.  */
        worker.onmessage = function (e) {
          completion(e.data.jsonString, e.data.error);
        }

        /* Send a message to worker.  */
        worker.postMessage({
          'action': 'run',
          'host': host,
          'port': port,
          'userApi': userApi,
          'jsonString': jsonString
        });
      }
    }

    function start() {
      var tan = new Tanserver(document.getElementById("host").value,
                              document.getElementById("port").value);

      var api        = document.getElementById("api").value;
      var jsonString = document.getElementById("json").value;

      tan.getJSON(api, jsonString,
                  function(jsonString, err) {
        if (err != null) {
          document.getElementById("result").value = err;
          return;
        }

        document.getElementById("result").value = jsonString;
      });

      document.getElementById("header").value = `{"user_api":"${api}","json_length":${jsonString.length}}\\r\\n`;
      document.getElementById("body").value = jsonString;
    }
  </script>
  <p class="text_host">Host:</p> <input type="text" id="host" placeholder="tanserver.org">
  <p class="text_port">Port:</p> <input type="text" id="port" placeholder="2579">
  <p class="text_api">API:</p> <input type="text" id="api" placeholder="hello_world">
  <p class="text_json">JSON:</p> <textarea id="json" rows="3" cols="50" placeholder='{"hello":"world"}'></textarea>
  <br><br><br>
  <button class="getjson" onclick="start()">getJSON</button>
  <br><br><br>
  <h3>Result:</h3> <textarea id="result" rows="10" cols="50" readonly="true"></textarea>
  <br><br><br>
  <p>Header:</p> <textarea id="header" rows="10" cols="50" readonly="true"></textarea>
  <br><br><br>
  <p>Body:</p> <textarea id="body" rows="10" cols="50" readonly="true"></textarea>
</body>

</html>