<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>AI Image and Prompt Input</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
      text-align: center;
    }
    form {
      max-width: 400px;
      margin: auto;
    }
    input, button {
      margin: 10px 0;
      padding: 10px;
      width: 100%;
      box-sizing: border-box;
    }
    .image-preview {
      margin-top: 10px;
      max-width: 100%;
      height: auto;
      border: 1px solid #ddd;
    }
  </style>
</head>
<body>
  <h1>Submit Your Inputs</h1>
  <form id="inputForm">
    <label for="image1">Upload Image 1:</label>
    <input type="file" id="image1" name="image1" accept="image/*" required>
    <img id="preview1" class="image-preview" alt="Preview of Image 1">

    <label for="image2">Upload Image 2:</label>
    <input type="file" id="image2" name="image2" accept="image/*" required>
    <img id="preview2" class="image-preview" alt="Preview of Image 2">

    <label for="prompt">Enter Prompt:</label>
    <input type="text" id="prompt" name="prompt" placeholder="Type your prompt here..." required>

    <button type="submit">Submit</button>
  </form>

  <div id="response" style="margin-top: 20px;"></div>

  <script>
    // Preview image 1
    document.getElementById('image1').addEventListener('change', (event) => {
      const file = event.target.files[0];
      const preview = document.getElementById('preview1');
      if (file) {
        preview.src = URL.createObjectURL(file);
        preview.style.display = 'block';
      } else {
        preview.src = '';
        preview.style.display = 'none';
      }
    });

    // Preview image 2
    document.getElementById('image2').addEventListener('change', (event) => {
      const file = event.target.files[0];
      const preview = document.getElementById('preview2');
      if (file) {
        preview.src = URL.createObjectURL(file);
        preview.style.display = 'block';
      } else {
        preview.src = '';
        preview.style.display = 'none';
      }
    });

    // Form submission
    document.getElementById('inputForm').addEventListener('submit', async (event) => {
      event.preventDefault();

      const formData = new FormData();
      formData.append('image1', document.getElementById('image1').files[0]);
      formData.append('image2', document.getElementById('image2').files[0]);
      formData.append('prompt', document.getElementById('prompt').value);

      try {
        const response = await fetch('https://your-backend-endpoint.com/process', {
          method: 'POST',
          body: formData,
        });

        const result = await response.json();
        document.getElementById('response').innerHTML = `<p>${result.message}</p>`;
      } catch (error) {
        console.error('Error:', error);
        document.getElementById('response').innerHTML = `<p>There was an error processing your request.</p>`;
      }
    });
  </script>
</body>
</html>
