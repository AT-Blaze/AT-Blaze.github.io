---
title: "Parker Chirps Since Silly Season"
# url: "/12/Parker Chirps"
draft: false
---

<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Flashing Number</title>
	<style>
	/*
		body {
			position: relative;
			height: 100vh;
			margin: 0;
			background-color: #000;
			color: #fff;
		}
	*/
		#flashingNumber {
			font-size: 10em;
			position: absolute;
			top: 50%;
			left: 50%;
			/*transform: translate(-50%, -50%);*/
			text-align: center;
			vertical-align: middle;
			height: 100px;
			line-height: 100px;
		}
	</style>
</head>

<body>

<!-- Create a container for the flashing number -->
<div id="flashingNumber"</div>

<script>
    // Function to generate a random color in hex format
    function getRandomColor() {
        const letters = '0123456789ABCDEF';
        let color = '#';
        for (let i = 0; i < 6; i++) {
            color += letters[Math.floor(Math.random() * 16)];
        }
        return color;
    }

    // Function to update the number with a flashing effect
    function flashNumber() {
        const numberElement = document.getElementById('flashingNumber');
        let chirps = 19;

        // Use setInterval to change the number color at regular intervals
        const intervalId = setInterval(() => {
            // Set a random color
            numberElement.style.color = getRandomColor();

            // Update the number (you can use your own logic here)
            numberElement.innerHTML = chirps;

            // Clear the interval after a certain number of iterations
            if (count === 20) {
                clearInterval(intervalId);
            }
        }, 100); // Change color every 500 milliseconds (adjust as needed)
    }

    // Call the function to start the flashing effect
    flashNumber();
</script>

</body>
</html>

