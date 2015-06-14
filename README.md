A apex classes with invocable methods to allow Process Builder to do more broadly applicable stuff

<a href="https://githubsfdeploy.herokuapp.com?owner=mshanemc&repo=processBuilderBlocks">
  <img alt="Deploy to Salesforce"
       src="https://raw.githubusercontent.com/afawcett/githubsfdeploy/master/src/main/webapp/resources/img/deploy.png">
</a>

Contents:
* **PBBSharing**
 * pass it a record Id, a user/group id, and an optional access level and it creates the sharing
 * known to support custom objects and some permutations of account (there's lots of complexity on account and I haven't tested them all)
 * I didn't write a test for this one--there's not guarantee that an org will have any __c custom object that this stuff depends on.
* **PBBAddPermSet**
 * pass it a permission set id and a user id, and it assigns that permission set to the user 
 * uses an @future method to avoid mixed DML issues
 * There is a test class for this one, because every org will have PermissionSets available. 
 * Because I did the testing, it's all nicely bulkified
*PBBDashboardRefresh
 * Refresh a dashboard from Process Builder (say, when opportunities change stage, you want anyone see the dashboard to have the lastest update!)
 * Requires a remote site setup for self-calls (ex: if you're na16.salesforce.com, then there's a remote site for that)
 * no error handling--fails silently if the call gets 401, 404, bad request, limits hit, etc
 * does handle bulk scenarios (built in batching)
 * no tests since I can't programmatically create a dashboard OR make callouts to get your actual dashboards from apex test