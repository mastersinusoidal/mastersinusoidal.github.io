---
layout: default
title: Gaurav Joshi
permalink: /project/suspension-atv/
---

<!-- Inline CSS for customization -->
<style>
    .responsive-img {
            width: 85%;
            max-width: 400px; /* Maximum width for larger screens */
            height: auto; /* Maintain aspect ratio */
        }
     .caption {
            font-family: 'Lato', sans-serif; /* Change this to any font you prefer */
            font-size: 14px;
            text-align: center;
            margin-top: 10px;
     }
  body {
      font-family: Arial, sans-serif;
      background-color: #FFFFFF;
      color: #333;
      margin: 0; /* Remove default margin */
      padding: 0; /* Remove default padding */
  }

  .content {
      margin: 20px auto; /* Center the content with auto margins */
      max-width: 800px; /* Set a maximum width for large screens */
      padding: 20px; /* Add padding around the content */
      background-color: #fff; /* Background color for the content area */
      box-shadow: 0 0 0px rgba(0, 0, 0, 0); /* Add a subtle shadow */
  }

  h1, h2, h3 {
      color: #000000;
      margin-top: 20px; /* Set top margin for headings */
  }

  p {
      text-align: justify;
      margin-bottom: 15px; /* Set bottom margin for paragraphs */
  }

  a {
      color: #000000;
      text-decoration: none;
  }

  a:hover {
      text-decoration: underline;
  }

  /* Responsive design for smaller screens */
  @media (max-width: 600px) {
      .content {
          margin: 10px; /* Reduce margin for smaller screens */
          padding: 15px; /* Reduce padding for smaller screens */
      }

      h1, h2, h3 {
          margin-top: 15px; /* Reduce top margin for headings on smaller screens */
      }

      p {
          margin-bottom: 10px; /* Reduce bottom margin for paragraphs on smaller screens */
      }
  }
    table {
      width: 100%;
      border-collapse: collapse;
      margin: 20px 0;
      font-size: 8px;
      text-align: left;
    }
    th, td {
      padding: 5px;
      border-bottom: 1px solid #ddd;
    }
    th {
      background-color: #f2f2f2;
      color: #333;
    }
    tr:nth-child(even) {
      background-color: #f9f9f9;
    }
    tr:hover {
      background-color: #f1f1f1;
    }

    /* Responsive styling */
    @media only screen and (max-width: 600px) {
      table, thead, tbody, th, td, tr {
        display: block;
      }
      thead tr {
        position: absolute;
        top: -9999px;
        left: -9999px;
      }
      tr {
        border: 1px solid #ccc;
        margin-bottom: 10px;
      }
      td {
        border: none;
        border-bottom: 1px solid #eee;
        position: relative;
        padding-left: 50%;
        text-align: right;
      }
      td:before {
        position: absolute;
        top: 12px;
        left: 12px;
        width: 45%;
        padding-right: 10px;
        white-space: nowrap;
        text-align: left;
        font-weight: bold;
      }
    }

.video-container {
    position: relative;
    padding-bottom: 56.25%;
    height: 0;
    overflow: hidden;
    max-width: 100%;
    margin: 0 auto;
}

.video-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    border: 0;
}

@media screen and (max-width: 600px) {
    .video-container {
        padding-bottom: 75%;
    }
}

</style>


<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
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
