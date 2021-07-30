- **/etc/init.d tanserver start**

`Description: `Start tanserver.  
`Availability: `1.0.0+

---

- **/etc/init.d tanserver status**

`Description: `Check the status.  
`Note: `If the server is running, it will include uptime, active connections and handled requests.  
`Availability: `1.0.0+

---

- **/etc/init.d tanserver reload**

`Description: `Reload user APIs.  
`Note 1: `This feature can be used in a production environment.  
`Note 2: `If reload fails, an error message will be displayed on the screen, which will not cause negative effects.  
`Availability: `1.0.0+

---

- **/etc/init.d tanserver stop**

`Description: `Stop tanserver.  
`Note: `The worker processes will exit after processing all events, so it is safe.  
`Availability: `1.0.0+

---

- **/etc/init.d tanserver restart**

`Description: `Restart tanserver.  
`Note: `This will apply the new configuration.  
`Availability: `1.0.3+

---

- **/etc/init.d tanserver configtest**

`Description: `Test configuration.  
`Note: `This does not test whether the database connection is available.  
`Availability: `1.0.0+

---

- **/etc/init.d tanserver version**

`Description: `Check the version.  
`Availability: `1.0.0+
