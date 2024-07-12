---
layout: default
title: Home
permalink: /project/material-characterization/
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Experimental studies on microstructural and corrosion characterisation of additively manufactured AISI 316 L austenitic stainless steel
</title>
</head>
<!-- Inline CSS for customization -->
<style>
        /* CSS for larger screens */
        @media (min-width: 601px) {
            .content {
                margin: auto;
                width: 80%;
            }
        }

        /* CSS for mobile screens */
        @media (max-width: 600px) {
            .content {
                margin: auto;
                width: 100%;
            }
        }
    </style>
<body>
    <div class="content" id="content"></div>

    <script>
        // Function to load content from an external file
        function loadContent() {
            fetch('content.html')
                .then(response => response.text())
                .then(data => {
                    document.getElementById('content').innerHTML = data;
                })
                .catch(error => console.error('Error loading content:', error));
        }

        // Load the content when the page loads
        window.onload = loadContent;
    </script>
</body>
</html>
