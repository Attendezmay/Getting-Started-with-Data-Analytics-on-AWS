
<body>

<h1 id="building-a-simple-aws-cloudtrail-data-analytics-solution">Building a Simple AWS CloudTrail Data Analytics Solution</h1>
<p>The next video demonstrates the steps that are listed here, This document includes the step-by-step instructions that Raf completes on the Part 3 of the demo you are about to watch. You can use this document as a reference guide, or follow up in your own AWS account, which might incur some costs and is not mandatory for completing the course.</p>
<p><strong>Important:</strong> If you choose to use your own account, make sure that you shut down the AWS resources you created after you finish using them, this is the last part of the demo.</p>

<h2 id="step-3-visualizing-athena-data-in-quicksight">Part 3: Visualizing Athena data in QuickSight</h2>
<p>The next video demonstrates the following steps. If you prefer to read instead of following a video, you can use this document as a reference guide. This document includes the step-by-step instructions that Raf completes on the final part of the demo you are about to watch!</p>
<ol type="1">
<li><p>As an AWS administrator: In the AWS Management Console, open the list of all AWS services by choosing <strong>Services</strong>, and locate and choose <strong>QuickSight</strong>.</p></li>
<li><p>If this is your first time logging in to QuickSight, you need to sign up for a subscription. To do so, choose <strong>Sign up for QuickSight</strong>, choose the <strong>Standard</strong> subscription, and choose <strong>Continue</strong>.</p></li>
<li><p><strong>Important:</strong> Remember to unsubscribe from QuickSight after you complete these instructions. You might incur costs from running QuickSight in your account.</p></li>
<li><p>For <strong>QuickSight account name</strong>, enter a globally unique name. As a suggestion, you can use <em>&lt;</em>your-initials<em>&gt;-analytics-demo-001</em> or some other unique value.</p></li>
<li><p>In the <strong>Notification email address</strong> box, enter a valid email address.</p></li>
<li><p>In the following check boxes below, select <strong>Amazon S3</strong>. A new <strong>Select Amazon S3 buckets</strong> window will open. In this window, select all the S3 buckets that are related to Athena and CloudTrail and choose <strong>Finish</strong>.</p></li>
<li><p>Back in the QuickSight page, choose <strong>Finish</strong>. Your QuickSight account will be created and ready to use. To start creating visualizations, choose <strong>Go to Amazon QuickSight</strong>.</p></li>
<li><p>In the navigation pane, choose <strong>Datasets</strong>, and in the upper-right area of the screen, choose <strong>New dataset</strong>.</p></li>
<li><p>From the data sources list, choose <strong>Athena</strong>. For <strong>Data source name</strong>, enter <em>athena1</em>, then choose <strong>Create data source</strong>.</p></li>
<li><p>Next, choose the Athena table in CloudTrail that you created in Part 2. Choose <strong>Select</strong>. On the next screen, choose <strong>Directly query your data</strong> and then choose Visualize.</p></li>
<li><p>You need to give QuickSight the permissions to access Amazon S3, or the queries will fail. You can do so by choosing Admin, and in the upper-right corner, choosing <strong>Manage QuickSight</strong>.</p>
<p><img src="images/image3.png" /></p></li>
<li><p>On the sidebar, choose <strong>Security &amp; permissions</strong>. Then, in the <strong>QuickSight access to AWS services</strong> option, choose <strong>Add or remove</strong>, select <strong>Amazon S3</strong>, and select all the related Athena and CloudTrail buckets. QuickSight can now access Athena to run queries. QuickSight can also access Amazon S3 to read the data through Athena</p></li>
<li><p>Return to the visualization by going to the upper-left area of the window and choosing the QuickSight logo.</p></li>
<li><p>In the <strong>Fields</strong> list, choose <strong>eventname</strong>. QuickSight will run an Athena query and populate a visualization, which should look like this example:</p>
<p><img src="images/image4.png" /></p></li>
<li><p>You will now create a new QuickSight dataset that focuses on the actions of the user <em>nicholas</em> because you want to get all the information that is related to them. In the upper-left corner, choose the QuickSight logo, then from the navigation pane, choose <strong>Datasets</strong>.</p></li>
<li><p>Go to the upper-right corner, choose <strong>New dataset</strong>, then choose Athena. For <strong>Data source name</strong>, enter <em>athena2</em> and then choose <strong>Create data source</strong>.</p></li>
<li><p>Next, choose <strong>Use custom SQL</strong> and for the custom SQL query name, enter <em>nicholas-activity</em>. Copy the following query and paste it as the custom SQL query, replacing <em>YOUR-ATHENA-TABLE-HERE</em> with your Athena table name. After you paste and update the SQL, choose <strong>Confirm query</strong>.</p>
<div class="sourceCode" id="cb3"><pre class="sourceCode sql"><code class="sourceCode sql"><a class="sourceLine" id="cb3-1" title="1"><span class="kw">SELECT</span> <span class="op">*</span></a>
<a class="sourceLine" id="cb3-2" title="2"><span class="kw">FROM</span></a>
<a class="sourceLine" id="cb3-3" title="3">    YOUR<span class="op">-</span>ATHENA<span class="op">-</span><span class="kw">TABLE</span><span class="op">-</span>HERE</a>
<a class="sourceLine" id="cb3-4" title="4"><span class="kw">WHERE</span></a>
<a class="sourceLine" id="cb3-5" title="5">    useragent <span class="kw">LIKE</span> <span class="st">&#39;%console%&#39;</span> <span class="kw">AND</span></a>
<a class="sourceLine" id="cb3-6" title="6">    useridentity.username <span class="kw">LIKE</span> <span class="st">&#39;nicholas&#39;</span>;</a></code></pre></div></li>
<li><p>Choose <strong>Directly query your data</strong> and then choose <strong>Visualize</strong>. You now have a dedicated QuickSight dataset that filters for all data under that query scope.</p></li>
<li><p>In the visualization, choose <strong>errorcode</strong>. You will see a bar chart of activities with a <code>GROUP BY errorcode</code>. It should look like this example:</p>
<p><img src="images/image5.png" /></p></li>
<li><p>To transform that information into a pie chart, go to the <strong>navigation pane &gt; Visual types</strong> and choose the pie chart icon.</p></li>
<li><p>When you are finished with these demo steps, unsubscribe from QuickSight and shut down all the other AWS resources you created.</p></li>
</ol>

</body>
</html>
