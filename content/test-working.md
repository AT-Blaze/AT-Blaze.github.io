---
title: "test"
draft: true
---
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Screen and Browser Information</title>
</head>
<body>

<!-- Container for displaying information -->
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
            <p>Screen Size: ${screenWidth} x ${screenHeight}</p>
            <p>Browser: ${browserName} ${browserVersion}</p>
        `;
    }

    // Call the function to display information when the page loads
    displayInfo();
</script>

<div id="ip-container"></div>

<script>
const apiKey = '2559268d50eada'
let lastRequestTime = 0;
	function getIpAddress() {
		const currentTime = Date.now();

    	// Make a request to ipinfo.io to get the user's IP address
    	fetch('https://ipinfo.io?token=2559268d50eada')
        	.then(response => response.json())
        	.then(data => {
            	// Extract and display the IP address from the response
            	const ip = data.ip || 'N/A';
				const city = data.city || 'unknown';
				const infoContainer = document.getElementById('info-container');
				infoContainer.innerHTML = `
				<p>Location: ${city}</p>
				<p>IP Address: ${ip}</p>
				`
        	})
        	.catch(error => console.error('Error:', error));
	}
	getIpAddress();
</script>

</body>
</html>

