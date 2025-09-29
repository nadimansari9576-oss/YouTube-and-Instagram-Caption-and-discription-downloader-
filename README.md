<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Instagram/YouTube Caption Extractor</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        .container {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        input, textarea, button {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
        }
        button {
            background-color: #007bff;
            color: white;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
        .result {
            margin-top: 20px;
            padding: 15px;
            background-color: #f8f9fa;
            border-radius: 5px;
            display: none;
        }
        .copy-btn {
            background-color: #28a745;
            width: auto;
            padding: 8px 15px;
        }
        .copy-btn:hover {
            background-color: #218838;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Instagram/YouTube Caption Extractor</h1>
        
        <input type="text" id="videoUrl" placeholder="Instagram Reel या YouTube Short का URL paste करें">
        <button onclick="extractCaption()">Caption Extract करें</button>
        
        <div class="result" id="result">
            <h3>Extracted Text:</h3>
            <textarea id="captionText" rows="6" readonly></textarea>
            <button class="copy-btn" onclick="copyToClipboard()">Copy Text</button>
            <span id="copyMessage" style="color: green; margin-left: 10px;"></span>
        </div>
    </div>

    <script>
        async function extractCaption() {
            const url = document.getElementById('videoUrl').value;
            const resultDiv = document.getElementById('result');
            const captionText = document.getElementById('captionText');
            const copyMessage = document.getElementById('copyMessage');
            
            copyMessage.textContent = '';
            
            if (!url) {
                alert('कृपया URL दर्ज करें');
                return;
            }

            // Simple URL validation
            if (!url.includes('instagram.com') && !url.includes('youtube.com') && !url.includes('youtu.be')) {
                alert('कृपया सही Instagram या YouTube URL दर्ज करें');
                return;
            }

            try {
                // Show loading
                captionText.value = 'Caption extract हो रहा है...';
                resultDiv.style.display = 'block';

                // Note: Actual extraction would require backend API due to CORS restrictions
                // This is a simulated version
                
                let extractedText = '';
                
                if (url.includes('instagram.com')) {
                    extractedText = await simulateInstagramExtraction(url);
                } else if (url.includes('youtube.com') || url.includes('youtu.be')) {
                    extractedText = await simulateYouTubeExtraction(url);
                }
                
                captionText.value = extractedText;
                
            } catch (error) {
                captionText.value = 'Error: Caption extract नहीं हो पाया। कृपया manual copy करें।';
                console.error('Extraction error:', error);
            }
        }

        // Simulated extraction functions
        async function simulateInstagramExtraction(url) {
            // In real implementation, you would use Instagram API or web scraping
            return `Instagram Reel Caption Example:\n\nयह एक example Instagram Reel की caption है।\nआप इसे copy करके कहीं भी use कर सकते हैं।\n\n#instagram #reel #example`;
        }

        async function simulateYouTubeExtraction(url) {
            // In real implementation, you would use YouTube API
            return `YouTube Short Description Example:\n\nयह एक example YouTube Short की description है।\nइसमें video के बारे में पूरी जानकारी है।\n\nSubscribe करें और like करें!\n\n#youtube #short #video`;
        }

        function copyToClipboard() {
            const captionText = document.getElementById('captionText');
            const copyMessage = document.getElementById('copyMessage');
            
            captionText.select();
            captionText.setSelectionRange(0, 99999); // For mobile devices
            
            try {
                navigator.clipboard.writeText(captionText.value).then(() => {
                    copyMessage.textContent = '✓ Text copied successfully!';
                    setTimeout(() => {
                        copyMessage.textContent = '';
                    }, 3000);
                });
            } catch (err) {
                // Fallback for older browsers
                document.execCommand('copy');
                copyMessage.textContent = '✓ Text copied successfully!';
                setTimeout(() => {
                    copyMessage.textContent = '';
                }, 3000);
            }
        }

        // Allow pressing Enter in URL input
        document.getElementById('videoUrl').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                extractCaption();
            }
        });
    </script>
</body>
</html>
