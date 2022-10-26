
<h1 id="building-a-simple-aws-cloudtrail-data-analytics-solution">Building a Simple AWS CloudTrail Data Analytics Solution</h1>
<p>The next video demonstrates the steps that are listed here, This document includes the step-by-step instructions that Raf completes on the Part 2 of the demo you are about to watch. You can use this document as a reference guide, or follow up in your own AWS account, which might incur some costs and is not mandatory for completing the course.</p>
<p><strong>Important:</strong> If you choose to use your own account, make sure that you shut down the AWS resources you created after you finish using them, but only do so after finishing part 3.</p>

<h2 id="step-2-query-cloudtrail-data-in-amazon-athena">Part 2: Query CloudTrail data in Amazon Athena</h2>
<p>The next video demonstrates the following steps. If you prefer to read instead of following a video, you can use this document as a reference guide. This document includes the step-by-step instructions that Raf completes on the part 2 of the demo you are about to watch!</p>
<p>Oh no! People in your organization are saying that a web server was turned off and the website is now offline. Now, you will use CloudTrail data to investigate what happened and get evidence of the action, including:</p>
<ul>
<li>Who shut down the web server</li>
<li>When they shut it down</li>
<li>Where they shut it down from</li>
</ul>
<p>You will do this investigation by creating an Athena table that points to the S3 bucket that is used by your new CloudTrail configuration.</p>
<ol type="1">
<li><p>As an AWS administrator: In the AWS Management Console, open the list of all AWS services by choosing <strong>Services</strong>, and locate and choose <strong>CloudTrail</strong>.</p></li>
<li><p>In the navigation pane, choose <strong>Event history</strong>, and then choose <strong>Create Athena table</strong>.</p></li>
<li><p>In <strong>Storage location</strong>, choose the bucket you created as part of CloudTrail configuration. This action will update the structured query language (SQL) command that creates the table to use the corresponding bucket location.</p></li>
<li><p>Choose <strong>Create table</strong>.</p></li>
<li><p>You now have an Athena table with the same schema that is used by CloudTrail. The table points to the recently created S3 bucket that is used by CloudTrail.</p></li>
<li><p>As an AWS administrator: In the AWS Management Console, open the list of all AWS services by choosing <strong>Services</strong>, and locate and choose <strong>Athena</strong>.</p></li>
<li><p>If this is the first time you’re using Athena in this AWS account, you will need configure some settings. In the upper-right area of the window, choose <strong>Settings</strong>.</p></li>
<li><p>Then, select another S3 bucket for the Athena query result location by choosing the <strong>Select</strong> button. A bucket might have been automatically created for this purpose, so you might only need to select a bucket with a name that starts with <em>aws-athena-query-results</em>.</p></li>
<li><p>After you select the bucket, choose <strong>Save</strong>, and you are ready to do Athena queries.</p></li>
<li><p>To get the activity history of a given EC2 instance, run the following query. Make sure to replace the instance ID with your instance ID. You also need to replace <em>YOUR-ATHENA-TABLE-HERE</em> with the name of your Athena table. You can copy the table name from the navigation pane. The query looks like this example:</p>
<div class="sourceCode" id="cb1"><pre class="sourceCode sql"><code class="sourceCode sql"><a class="sourceLine" id="cb1-1" title="1"><span class="kw">SELECT</span> <span class="op">*</span></a>
<a class="sourceLine" id="cb1-2" title="2"><span class="kw">FROM</span></a>
<a class="sourceLine" id="cb1-3" title="3">    YOUR<span class="op">-</span>ATHENA<span class="op">-</span><span class="kw">TABLE</span><span class="op">-</span>HERE</a>
<a class="sourceLine" id="cb1-4" title="4"><span class="kw">WHERE</span> </a>
<a class="sourceLine" id="cb1-5" title="5">    eventsource <span class="op">=</span> <span class="st">&#39;ec2.amazonaws.com&#39;</span> <span class="kw">AND</span> </a>
<a class="sourceLine" id="cb1-6" title="6">    requestparameters <span class="kw">LIKE</span> <span class="st">&#39;%YOUR-INSTANCE-ID-HERE%&#39;</span> <span class="kw">AND</span></a>
<a class="sourceLine" id="cb1-7" title="7">    responseelements <span class="op">!=</span> <span class="st">&#39;null&#39;</span>;</a></code></pre></div></li>
<li><p>This query should reveal that the <em>nicholas</em> user issued an API call that shut down the web server. The following query shows you the other actions that <em>nicholas</em> did in the AWS account:</p>
<div class="sourceCode" id="cb2"><pre class="sourceCode sql"><code class="sourceCode sql"><a class="sourceLine" id="cb2-1" title="1"><span class="kw">SELECT</span> <span class="op">*</span></a>
<a class="sourceLine" id="cb2-2" title="2"><span class="kw">FROM</span></a>
<a class="sourceLine" id="cb2-3" title="3">    YOUR<span class="op">-</span>ATHENA<span class="op">-</span><span class="kw">TABLE</span><span class="op">-</span>HERE</a>
<a class="sourceLine" id="cb2-4" title="4"><span class="kw">WHERE</span></a>
<a class="sourceLine" id="cb2-5" title="5">    useragent <span class="kw">LIKE</span> <span class="st">&#39;%console%&#39;</span> <span class="kw">AND</span></a>
<a class="sourceLine" id="cb2-6" title="6">    useridentity.username <span class="kw">LIKE</span> <span class="st">&#39;nicholas&#39;</span>;</a></code></pre></div></li>
<li><p>You will now learn a way to visualize this information in Amazon QuickSight. Suppose that you want a pie chart of successful requests and failed requests. SQL is better than seeing the information in a text form. Part 3 covers creating visualizations to see a pie chart of the actions made by that user.</p></li>
</ol>


</script>
</body>
</html>
