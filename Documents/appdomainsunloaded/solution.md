## Possible Solutions
* If you want to make changes to your site, like updating a binary file, try deploying to a slot and then swapping with production instead of just placing a new dll in your production site
* To find the reason for the App Domain restarting add this to the app's web.config:
```
<system.web>
  <customErrors mode="Off" />
  <rules>
    <add name="Application Events"
         eventName="Application Lifetime Events"
         provider="EventLogProvider"
         profile="Default"
         minInterval="00:01:00" />
  </rules>
</system.web>
```
