# QR-code-generatorr
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advanced QR Code Generator</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #4361ee;
            --secondary: #3f37c9;
            --accent: #4cc9f0;
            --light: #f8f9fa;
            --dark: #212529;
            --success: #4bb543;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Poppins', sans-serif;
            background-color: #f5f7ff;
            color: var(--dark);
            line-height: 1.6;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }
        
        .container {
            max-width: 900px;
            margin: 2rem auto;
            padding: 0 1rem;
        }
        
        header {
            text-align: center;
            margin-bottom: 2rem;
        }
        
        h1 {
            color: var(--primary);
            font-size: 2.5rem;
            margin-bottom: 0.5rem;
            font-weight: 600;
        }
        
        .subtitle {
            color: #6c757d;
            font-size: 1.1rem;
        }
        
        .card {
            background: white;
            border-radius: 12px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            padding: 2rem;
            margin-bottom: 2rem;
        }
        
        .input-group {
            margin-bottom: 1.5rem;
        }
        
        label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 500;
            color: var(--dark);
        }
        
        input[type="text"], 
        textarea, 
        select {
            width: 100%;
            padding: 0.8rem 1rem;
            border: 2px solid #e9ecef;
            border-radius: 8px;
            font-size: 1rem;
            transition: border-color 0.3s;
        }
        
        input[type="text"]:focus, 
        textarea:focus, 
        select:focus {
            outline: none;
            border-color: var(--primary);
        }
        
        .options-row {
            display: flex;
            gap: 1rem;
            margin-bottom: 1.5rem;
        }
        
        .option-group {
            flex: 1;
        }
        
        button {
            background-color: var(--primary);
            color: white;
            border: none;
            padding: 0.8rem 1.5rem;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: 500;
            transition: all 0.3s;
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
        }
        
        button:hover {
            background-color: var(--secondary);
            transform: translateY(-2px);
        }
        
        button:active {
            transform: translateY(0);
        }
        
        .btn-secondary {
            background-color: #6c757d;
        }
        
        .btn-secondary:hover {
            background-color: #5a6268;
        }
        
        #qrcode-container {
            display: none;
            margin-top: 2rem;
            text-align: center;
        }
        
        #qrcode {
            margin: 0 auto;
            padding: 1rem;
            background: white;
            border-radius: 8px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            display: inline-block;
        }
        
        #qrcode img {
            max-width: 100%;
            height: auto;
        }
        
        .result-container {
            display: none;
            margin-top: 2rem;
            padding: 1.5rem;
            background: #f8f9fa;
            border-radius: 8px;
            border-left: 4px solid var(--primary);
        }
        
        .result-title {
            font-weight: 600;
            margin-bottom: 0.5rem;
            color: var(--primary);
        }
        
        .result-content {
            word-break: break-all;
        }
        
        .action-buttons {
            display: flex;
            gap: 1rem;
            margin-top: 1.5rem;
            justify-content: center;
        }
        
        footer {
            text-align: center;
            margin-top: auto;
            padding: 1.5rem;
            color: #6c757d;
            font-size: 0.9rem;
        }
        
        @media (max-width: 768px) {
            .options-row {
                flex-direction: column;
            }
            
            .action-buttons {
                flex-direction: column;
            }
            
            button {
                width: 100%;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>QR Code Generator</h1>
            <p class="subtitle">Create and scan QR codes instantly</p>
        </header>
        
        <div class="card">
            <div class="input-group">
                <label for="qr-content">Enter text, URL, or other content:</label>
                <textarea id="qr-content" rows="3" placeholder="https://example.com or any text you want to encode"></textarea>
            </div>
            
            <div class="options-row">
                <div class="option-group">
                    <label for="qr-size">Size:</label>
                    <select id="qr-size">
                        <option value="150x150">Small (150×150)</option>
                        <option value="250x250" selected>Medium (250×250)</option>
                        <option value="350x350">Large (350×350)</option>
                    </select>
                </div>
                
                <div class="option-group">
                    <label for="qr-color">Color:</label>
                    <select id="qr-color">
                        <option value="000000" selected>Black</option>
                        <option value="4361ee">Blue</option>
                        <option value="e63946">Red</option>
                        <option value="2a9d8f">Teal</option>
                    </select>
                </div>
            </div>
            
            <button id="generate-btn">
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
                    <path d="M2 1a1 1 0 0 0-1 1v12a1 1 0 0 0 1 1h12a1 1 0 0 0 1-1V2a1 1 0 0 0-1-1H2zM0 2a2 2 0 0 1 2-2h12a2 2 0 0 1 2 2v12a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2V2zm5.5 4a1.5 1.5 0 1 1-3 0 1.5 1.5 0 0 1 3 0zm4 0a1.5 1.5 0 1 1-3 0 1.5 1.5 0 0 1 3 0zM16 8a8 8 0 1 1-16 0 8 8 0 0 1 16 0zm-3-4a.5.5 0 0 1-.5.5h-9a.5.5 0 0 1 0-1h9a.5.5 0 0 1 .5.5z"/>
                </svg>
                Generate QR Code
            </button>
            
            <div id="qrcode-container">
                <div id="qrcode"></div>
                
                <div class="result-container" id="result-container">
                    <div class="result-title">Scan Result Preview:</div>
                    <div class="result-content" id="result-content"></div>
                </div>
                
                <div class="action-buttons">
                    <button id="download-btn" class="btn-secondary">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
                            <path d="M.5 9.9a.5.5 0 0 1 .5.5v2.5a1 1 0 0 0 1 1h12a1 1 0 0 0 1-1v-2.5a.5.5 0 0 1 1 0v2.5a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2v-2.5a.5.5 0 0 1 .5-.5z"/>
                            <path d="M7.646 11.854a.5.5 0 0 0 .708 0l3-3a.5.5 0 0 0-.708-.708L8.5 10.293V1.5a.5.5 0 0 0-1 0v8.793L5.354 8.146a.5.5 0 1 0-.708.708l3 3z"/>
                        </svg>
                        Download
                    </button>
                    <button id="new-btn">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
                            <path d="M8 0a8 8 0 1 1 0 16A8 8 0 0 1 8 0zM4.5 7.5a.5.5 0 0 0 0 1h5.793l-2.147 2.146a.5.5 0 0 0 .708.708l3-3a.5.5 0 0 0 0-.708l-3-3a.5.5 0 1 0-.708.708L10.293 7.5H4.5z"/>
                        </svg>
                        New QR Code
                    </button>
                </div>
            </div>
        </div>
    </div>
    
    <footer>
        <p>© 2023 QR Code Generator | Scan the code to view the encoded content</p>
    </footer>
    
    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const generateBtn = document.getElementById('generate-btn');
            const downloadBtn = document.getElementById('download-btn');
            const newBtn = document.getElementById('new-btn');
            const qrContent = document.getElementById('qr-content');
            const qrSize = document.getElementById('qr-size');
            const qrColor = document.getElementById('qr-color');
            const qrcodeContainer = document.getElementById('qrcode-container');
            const qrcodeDiv = document.getElementById('qrcode');
            const resultContainer = document.getElementById('result-container');
            const resultContent = document.getElementById('result-content');
            
            generateBtn.addEventListener('click', generateQRCode);
            downloadBtn.addEventListener('click', downloadQRCode);
            newBtn.addEventListener('click', resetForm);
            
            function generateQRCode() {
                const content = qrContent.value.trim();
                const size = qrSize.value;
                const color = qrColor.value;
                
                if (!content) {
                    alert('Please enter some content to generate a QR code');
                    return;
                }
                
                const encodedContent = encodeURIComponent(content);
                const qrCodeUrl = `https://api.qrserver.com/v1/create-qr-code/?size=${size}&color=${color}&data=${encodedContent}`;
                
                qrcodeDiv.innerHTML = `<img src="${qrCodeUrl}" alt="QR Code">`;
                qrcodeContainer.style.display = 'block';
                
                resultContent.textContent = content;
                resultContainer.style.display = 'block';
                
                // Scroll to the QR code
                qrcodeContainer.scrollIntoView({ behavior: 'smooth' });
            }
            
            function downloadQRCode() {
                const qrCodeImg = document.querySelector('#qrcode img');
                if (!qrCodeImg) return;
                
                const link = document.createElement('a');
                link.href = qrCodeImg.src;
                link.download = `qrcode-${Date.now()}.png`;
                document.body.appendChild(link);
                link.click();
                document.body.removeChild(link);
            }
            
            function resetForm() {
                qrContent.value = '';
                qrcodeContainer.style.display = 'none';
                resultContainer.style.display = 'none';
                qrContent.focus();
            }
        });
    </script>
</body>
</html>
