When submit the HTML form, it's default action is to post the form data to the server and leave the current page. Even Polymer IronForm can be configured to keep in the same page, but it does not support file in the form.  Here summarize the trick to submit the form in the same page with Polymer, not JQuery.   

For this HTML form:

```
	<form enctype="multipart/form-data">
		<input id='fileUploadInput' type="file" name="fileToUpload" id="fileToUpload" onchange="previewFile()">
		<input id='submitButton' type="submit" value="Upload Image" name="submit" onclick="postImg();">
	</form>
	<img id="previewImg" src="" height="200" alt="Image preview...">
```

Use HTML form to create [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData) as a container, then submit FormData by JavaScript through [XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/send) or 

HTML form element creates FormData more cleanly than manually create it by JavaScript,especially for file submit.  Here we have the form without action & method (such as: action="upload.html" method="post"), as the form container. 

'''
  function postImg(){
          var file = document.querySelector('#fileUploadInput').files[0]; 
          var formData = new FormData(document.querySelector('#uploadForm'));
          var xhr = new XMLHttpRequest();
          // Add any event handlers here...
          xhr.open('POST', '/api/image/process', true);
          xhr.onload = function(){
            var jsonResponse = JSON.parse(xhr.responseText);
            console.log(jsonResponse);
          }
          xhr.send(formData);
          return false; // To avoid actual submission of the form
       }
'''


If we want to show Image after uploading it. Add  onchange function (previewFile) for file input. In it, set img src to FileReader's result after loading the image file.

```
   function previewFile(){
       var preview = document.querySelector('#previewImg'); //selects the query named img
       var file    = document.querySelector('#fileUploadInput').files[0]; //sames as here
       var reader  = new FileReader();

       reader.onloadend = function () {
           preview.src = reader.result;
       }

       if (file) {
           reader.readAsDataURL(file); //reads the data as a URL
       } else {
           preview.src = "";
       }
  }
```
  
 To play around this code, copy the HTML & JavaScript code to [CodePen](https://codepen.io/pen).
