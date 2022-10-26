
<h1 id="building-a-simple-aws-cloudtrail-data-analytics-solution">Building a Simple AWS CloudTrail Data Analytics Solution</h1>
<h1 id="before-starting">Before starting</h1>
<p>The next video demonstrates the steps that are listed here, This document includes the step-by-step instructions that Raf completes on the Part 1 of the demo you are about to watch. You can use this document as a reference guide, or follow up in your own AWS account, which might incur some costs and is not mandatory for completing the course.</p>
<p><strong>Important:</strong> If you choose to use your own account, make sure that you shut down the AWS resources you created after you finish using them, but only do so after finishing part 3.</p>
<p>The demo will show how you can visualize AWS CloudTrail data in Amazon QuickSight and start building simple security dashboards. Although CloudTrail is enabled by default in every AWS Account, Raf will configure a new trail, and also to show where CloudTrail configurations are made.</p>
<p>After configuring a new trail, Raf will add a new user into his AWS account (named <em>nicholas</em>). He will then log in as that user and do some activity that simulates a user who is issuing application programming interface (API) calls. One of these API calls will (accidentally) turn off a web server. If you want to follow the exact instructions in your account, you can mimic the scenario that Raf has in his account before you enable CloudTrail. To do so, you can create an Amazon Elastic Compute Cloud (Amazon EC2) instance to function as the web server.</p>
<p>After Raf turns off the web server as the user <em>nicholas</em>, he will log out and log in again as an administrator. Raf will then he will use CloudTrail data to investigate what happened by getting information, such as when the server was turned off. He will also discover the other API calls that the <em>nicholas</em> user made, because that account could have been compromised.</p>
<p>If you prefer decide to follow the instructions in your own account, make sure that all your resources are created in the <strong>N. Virginia</strong> AWS Region. The AWS Region can be located on the upper-right area of the AWS Management Console.</p>
<p><img src="images/image.png" /></p>
<h2 id="step-1-configuring-cloudtrail-and-adding-a-secondary-iam-user">Part 1: Configuring CloudTrail and adding a secondary IAM User</h2>
<ol type="1">
<li><p>As an AWS administrator: In the AWS Management Console, open the list of all AWS services by choosing <strong>Services,</strong> and then locate and choose <strong>CloudTrail</strong>.</p></li>
<li><p>Choose <strong>Create trail</strong>.</p></li>
<li><p>For <strong>Trail name</strong>, enter <em>default</em>. If that Trail name already exists in your account, enter: <em>default_analytics</em></p></li>
<li><p>In the <strong>Trail log bucket and folder</strong> box, keep the default name suggestion. Note that this S3 bucket is the bucket where CloudTrail will store information. Make sure that you copy this bucket name because you will need it when you create the Amazon Athena table in Part 2.</p></li>
<li><p>Clear the <strong>Log file SSE-KMS</strong> encryption check box.</p></li>
<li><p>Scroll to the bottom of the page and choose <strong>Next</strong>.</p></li>
<li><p>On the next page, select <strong>Management events</strong>, <strong>Data events</strong>, and <strong>Insights events</strong>.</p></li>
<li><p>Scroll down to the bottom of the page and choose <strong>Next</strong>.</p></li>
<li><p>Review the information and choose <strong>Create trail</strong>.</p></li>
<li><p>You now have a new CloudTrail dataset that is being created in the designated bucket. You can go to Amazon S3 and inspect how the data structure will look like, as Raf did. As you interact with the AWS Management Console, your user is issuing API calls, which are captured and stored by CloudTrail.</p></li>
<li><p>As an AWS administrator: In the AWS Management Console, open the list of all AWS services by choosing <strong>Services</strong>, and locate and choose <strong>IAM</strong>.</p></li>
<li><p>In the navigation pane, choose <strong>Users</strong> and then choose <strong>Add user</strong>.</p></li>
<li><p>For the <strong>User name</strong> field, enter: <em>nicholas</em> (all lowercase).</p></li>
<li><p>For <strong>Access type</strong>, clear <strong>Programmatic access</strong> and select <strong>AWS Management Console access</strong>.</p></li>
<li><p>For <strong>Console password</strong>, choose <strong>Custom password</strong> and enter a password for the <em>nicholas</em> user.</p></li>
<li><p>Clear the <strong>User must create a new password at next sign-in</strong> check box and choose <strong>Next: Permissions</strong>.</p></li>
<li><p>On the <strong>Set permissions</strong> page, choose <strong>Attach existing policies directly</strong>.</p></li>
<li><p>In the <strong>Filter policies</strong> box, search for and select <strong>AmazonEC2FullAccess</strong> and <strong>AmazonS3FullAccess</strong>.</p></li>
<li><p>Choose <strong>Next: Tags</strong>, then choose <strong>Next: Review</strong>, and then choose <strong>Create user</strong>.</p></li>
<li><p>In the <strong>Success</strong> page, copy the displayed IAM sign-in URL, and then choose <strong>Close</strong>. If you inadvertently didn’t copy the URL, you can also locate it on the main IAM page by opening the IAM dashboard, as in the following screen capture:</p>
<p><img src="images/image1.png" /></p></li>
<li><p>Now you have a secondary IAM user (<em>nicholas</em>) that has the permissions to fully interact with Amazon EC2 and Amazon S3. Log out and log in as the new <em>nicholas</em> user by using the sign-in URL.</p></li>
<li><p>You can verify if you are logged in with the <em>nicholas</em> user by looking in the upper-right are of the AWS Management Console:</p>
<p><img src="images/image2.png" /></p></li>
<li><p>In the <em>nicholas</em> account, issue some API calls by navigating through the AWS Management Console. All your actions will be captured by CloudTrail.</p></li>
<li><p>While you are logged in to the console as <em>nicholas</em>, shut down an EC2 instance. Before you shut down any EC2 instances, make sure that you don’t need them, or that you created an additional EC2 instance specifically for this exercise.</p></li>
<li><p>Log out as <em>nicholas</em> and log back in as the administrator because you will next use Amazon Athena to query CloudTrail data!</p></li>
</ol>

<script>
document.body.innerHTML = document.body.innerHTML.replace(/RELATIVE(.+)RELATIVE/g, function (match, capture) {
  let tmp = document.createElement("DIV");
  tmp.innerHTML = capture;
  return new URL(tmp.textContent || tmp.innerText || "", document.baseURI).href;
});
</script>
</body>
</html>
