# NOT MAINTAINED

# ti.tesstwo
Appcelerator Titanium module for simple OCR, based on 'tess-two' android module (Tesseract)

Compiled with titanium SDK 6.0.1 (only english trained file included).

# Methods and parameters
Main method - GetOcr(image, whitelist, blacklist)

image - Image as BLOB!

whitelist - letters white list for OCR filtering

blacklist - letters black list for OCR filtering

N/B if you are using GetOcr without white or blacklist, pass empty string ''. Example: ocrlib.GetOcr(tmpImg, '', '')

# Example usage
```JavaScript
var ocrlib = require('ru.everapp.tessocr');

//Get OCR text from ImageView
function FromImgView(e) {
	  var tmpImg = $.image.toBlob();
		var result = '';
		try{
			result = ocrlib.GetOcr(tmpImg, '', '');
		}catch(ex){
		  console.log(ex);
		}
    tmpImg = null;
    
    return result;
}

//Get text from image in ImageView
var TextFromImageView = FromImgView();
```

```JavaScript
var ocrlib = require('ru.everapp.tessocr');

//Get OCR text from camera picture (check camera permissions not included)
function OCRFromCamera(e){
	Titanium.Media.showCamera({
		success:function(event) {
			// called when media returned from the camera
			Ti.API.debug('Our type was: '+event.mediaType);
			if(event.mediaType == Ti.Media.MEDIA_TYPE_PHOTO) {
          var tmpImgc = event.media;
          var result = '';
          try{
            result = ocrlib.GetOcr(tmpImgc, 'aAbBcCdDeEfFgGhHiIjJkKlLmMnNoOpPqQrRsStTuUvVwWxXyYzZ1234567890\'"-=+,.?;/ ', '');
          }catch(ex){
            console.log(ex);
          }
          //Show simple OCR result in alert
			    alert(result);
          //
          tmpImgc = null;
			} else {
				alert("got the wrong type back ="+event.mediaType);
			}
		},
		cancel:function() {
			// called when user cancels taking a picture
		},
		error:function(error) {
			// called when there's an error
			var a = Titanium.UI.createAlertDialog({title:'Camera'});
			if (error.code == Titanium.Media.NO_CAMERA) {
				a.setMessage('Please run this test on device');
			} else {
				a.setMessage('Unexpected error: ' + error.code);
			}
			a.show();
		},
		saveToPhotoGallery:false,
		allowEditing: false,
		mediaTypes: [Ti.Media.MEDIA_TYPE_PHOTO]
	});
}

//Get text from camera picture
OCRFromCamera(); 
```
