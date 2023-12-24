---
title: "Should you use a VPN?"
date: 2023-12-24T02:48:32
draft: false
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Screen and Browser Information</title>
</head>
<body>

<div id="ip-container"></div> 
<div id="info-container"></div> 

<script>
    // Function to get and display screen and browser information
    function displayInfo() {
        // Get screen information
        const screenWidth = window.screen.width;
        const screenHeight = window.screen.height;

        // Get browser information
        const browserName = navigator.appName;
        const browserVersion = navigator.appVersion;
		
        // Display information in the container
        const infoContainer = document.getElementById('info-container');
        infoContainer.innerHTML = `
            <p>Your screen size: ${screenWidth} x ${screenHeight}</p>
            <p>Your browser: ${browserName} ${browserVersion}</p>
        `;
    }

    displayInfo();

const apiKey = '2559268d50eada'

	function getIpAddress() {
    	fetch('https://ipinfo.io?token=2559268d50eada')
        	.then(response => response.json())
        	.then(data => {
            	// Extract and display the IP address from the response
            	const ip = data.ip || 'unknown';
				const city = data.city || 'unknown';
				const ipContainer = document.getElementById('ip-container');
				ipContainer.innerHTML = `
					<p>Your apparent location: ${city}</p>
					<p>Your IP Address: ${ip}</p>
				`;
        	})
        	.catch(error => console.error('Error:', error));
	}
	getIpAddress();
</script>
(If you don't see much here then your browser or an extension is blocking some or all of the javascript i've written, good!)
_______________________________________________

I personally think that info above is pretty spooky for just anyone to have. Of course its not that big of a deal for something like amazon to have, obviosly they will need to know where you are browsing from. And of course, your screen size, that will be relevant to any streaming service that wants to know what size movie they can show you. 

Of course those things are important for certain people to know, but I know them. Do I need to know your address for you to read my blog? Certainly not... If I wanted to I could get your exact latitude and longitude. There's no need for all that. Thats why I think people should use VPNs, because, though you need to have an IP address, does everyone really need to know YOUR IP address? If you use a VPN then you share an IP address with many other people that obfuscates your real location. 

As for screen size and browser information, thats more complicated to change, but its certainly possible. In fact, its one of the only things that agencies with a desire to censor people using Tor can use. They'll frequently identify people by identifying what device theyre using, or their screen size. If you actually want to hide all that, try the Tails operating system that journalists can use that runs off a USB drive. 

Anyway, more people should use VPNs because theres no need for all that info about your browsing to be in the hands of anyone running a website you connect to. Especially when its used to collect advertisment data thats sold without your knowledge. The big thing is that many services now blacklist IP addresses that come from known Tor exit nodes, or even from VPN services (or just annoying reCAPTCHAs). The more people use them, the more likely it is that theyll stop blacklisting everyone and maybe someday theyll get the hint that we dont really want to be tracked all the time!

This is also mostly just another excuse for me to try written my own javascript.

</body>
</html>

