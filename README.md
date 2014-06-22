SocialGap
=========

SocialGap is a simple library intended to ease the integration of PhoneGap hybrid mobile apps with social networks.
It is modular, so it can be easily extended and it reduces overhead since you import only the modules you need.
This plugin has been developed as a proof of concept while developing Mmarazzu Mobile app.
This software is not intended for production usage as it is because of the following list of known needed modifications:

<ol>
	<li> 
		Facebook long-lived token support needs the app-secret. This should not be deployed on the clients. 
		In order to use the Facebook API as intended you need to transform short-lived token in long-lived 
		ones on your servers and then transport the tokens on the clients, where they will be stored.
	</li>
</ol>

Setup
-------

Including this library in your project is quite easy.
This software require the <a href="https://github.com/apache/cordova-plugin-inappbrowser/blob/master/doc/index.md" target="_blank">inAppBrowser</a> plugin and the <a href="http://modernizr.com/" target="_blank">modernizr</a> javascript library. <br>

If you do not have it already, you can install the inAppBrowser plugin by typing the following command from within your app main folder: <br>
<code>cordova plugin add https://git-wip-us.apache.org/repos/asf/cordova-plugin-inappbrowser.git</code> <br>

Once the prerequisites are in place, reference the following js files from your html page:
 <pre><code>	&lt;script type=&quot;text/javascript&quot; src=&quot;js/modernizr.js&quot;&gt;&lt;/script&gt;
	&lt;script type=&quot;text/javascript&quot; src=&quot;js/SocialGap/socialGap.js&quot;&gt;&lt;/script&gt;
	&lt;script type=&quot;text/javascript&quot; src=&quot;js/SocialGap/socialGap_facebook.js&quot;&gt;&lt;/script&gt;</code></pre>

Then notify the SocialGap library that the <code>onDeviceReady</code> event has been received.
This should look something like the following:

 <pre><code>	onDeviceReady: function() {
		...
		SocialGap.deviceReady = true;
		....
    }</code></pre>

From now on the setup procedure differ based on the module you would like to use.

<ul>
	<li><b>Facebook</b>:<br>
		Fill out the required settings in the file called <code>socialGap_facebook.js</code>.<br>
		You need to modify the object called <code>settings</code> that looks like the following:<br>
		<pre><code>	/* !!! Modify the following settings !!! */
	var settings = {
		appID: "123456789012345",
		appSecret: "12345678901234567890123456789012",
		appDomain: "http://yanchware.com",
		scopes: "email,publish_stream"
	};</code></pre><br>
		
		Then prepare two callback functions.<br>
		One of them will be called in case of success receiving as parameter the facebook access token.<br>
		Instead, the other will be called in case of failure.
		 <pre><code>	fbLogonSuccess: function(accessToken)
	{
		alert(token);
	}

	fbLogonFailure: function(){
		alert('Fail');
	}</code></pre>
		
		Once ready build a link that will start the authentication process.
		 <pre><code>	&lt;a onclick=&quot;SocialGap.Facebook_PerformLogon(fbLogonSuccess, fbLogonFailure);&quot;&gt;
		Facebook
	&lt;/a&gt;</code></pre>
		
	</li>
</ul>

Develop an extension
---------------------
Developing an extension is quite straightforward. <br>
We have prepared a "template" in <code>example/js/socialGap_basic.js</code> which can be used as a starting point for extending this library.

Run the example
-------
In order to make the example work follow these steps:
<ol>
	<li> Create a new PhoneGap app typing something similar to:<br>
   		<code>phonegap create YourApp/ com.whatever.yourapp YourApp</code></li>
		<li> Copy the files contained in the <code>example</code> folder into the <code>www</code> folder of the project you've just created</li>
		<li> Copy the folder <code>Social Gap</code> contained under the <code>lib</code> directory into the folder <code>www/js</code> of the project you have just created.</li>
		<li>Set the required settings in the modules (for instance in socialGap_facebook.js).</li>
		<li>Install the <a href="https://github.com/apache/cordova-plugin-inappbrowser/blob/master/doc/index.md" target="_blank">inAppBrowser</a> plugin for your project, typing these commands:
			<pre><code>cd YourApp
cordova plugin add https://git-wip-us.apache.org/repos/asf/cordova-plugin-inappbrowser.git</code></pre>			
		</li>
		<li> 
			Run the project for the platform you like most. <br>
			For instance type the following command from within <code>YourApp</code> directory:<br/>
   			<code>phonegap run android</code>
		</li>
</ol>
