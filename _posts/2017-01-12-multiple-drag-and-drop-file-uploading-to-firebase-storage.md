---
layout: post
title:  Multiple drag and drop file uploading to firebase storage
excerpt: "Jquery easy file upload to firebase storage"
categories: [Firebase, Storage, File, Upload]
comments: true
tags:
    - NoSQL databases
    - Firebase
    - File
    - multiple
    - drag and drop
    - Storage
    - Google Cloud Storage
---

In this upload example, I have explained how to implement drag and drop file upload using HTML5 and jQuery with firebase multiply file upload.

#### Firebase Storage

<div class="row">
<div class="col-md-6">
<div class="embed-responsive embed-responsive-16by9">
<iframe class="embed-responsive-item" src="https://www.youtube.com/embed/_tyjqozrEPY" frameborder="0" allowfullscreen></iframe>
</div>
</div>
<div class="col-md-6" markdown="1">
<p style="margin-top: 0px;">Firebase Storage is built for app developers who need to store and serve user-generated content, such as photos or videos.</p>

<p style="margin-top: 0px;">Firebase Storage adds Google security to file uploads and downloads for your Firebase apps, regardless of network quality. 
You can use it to store images, audio, video, or other user-generated content. 
Firebase Storage is backed by Google Cloud Storage, a powerful, simple, and cost-effective object storage service.</p>
Read more:  [Firebase Storage](https://firebase.google.com/docs/storage/)
</div>
</div>

### Getting Started
<strong> First we need to first create some HTML ready to handle file upload from the system to Firebase </strong>

![image-title-here](/assets/img/drop.png){:class="img-responsive"}

<strong>Step 1</strong> Follow the steps to make drag and drop file upload as shown in the above image.

{% highlight html %}
<form class="box" method="post" action="" enctype="multipart/form-data">
    <div id="drop-zone">
        <div class="drop-zone-caption">Drag & Drop Files Here</div>
        <span class="btn btn-primary btn-file" style="position: relative">
            <span>Choose files</span>
            <input type="file"id="drop-zone-file" name="files[]" multiple>
        </span>
    </div>
</form>
{% endhighlight %}

<strong>Step 2</strong> We can add some style to div using below CSS

{% highlight css %}
    #dragandrophandler {
        border: 2px dotted #0B85A1;
        width: 400px;
        color: #92AAB0;
        text-align: left;
        vertical-align: middle;
        padding: 10px 10px 10px 10px;
        margin-bottom: 10px;
        font-size: 200%;
    }

    #drop-zone {
        width: 360px;
        height: 240px;
        text-align: center;
        padding: 86px 0 0;
        outline: 2px dashed #92b0b3;
        outline-offset: -10px;
        -webkit-transition: outline-offset .15s ease-in-out, background-color .15s linear;
        transition: outline-offset .15s ease-in-out, background-color .15s linear;
        font-size: 1.25rem;
        background-color: #c8dadf;
        /* position: relative; */
        /* padding: 100px 20px; */
    }

    .btn-file input[type=file] {
        position: absolute;
        left: 0;
        top: 0;
        height: 100%;
        width: 100%;
        opacity: 0;
        cursor: pointer;
    }

    input[type=file] {
        display: block;
    }

    #drop-zone .drop-zone-caption {
        font-size: 20px;
        font-weight: 600;
        color: #919fa9;
        margin: 0 0 14px;
    }

    .btn.btn-primary {
        background-color: #00a8ff;
        border-color: #00a8ff;
    }
{% endhighlight %}

<strong>Step 3</strong> Handle drag and drop events with jQuery

{% highlight javascript %}
var obj = $("#drop-zone");
obj.on('dragenter', function (e) {
    e.stopPropagation();
    e.preventDefault();
    $(this).css('border', '2px solid #0B85A1');
});
obj.on('dragover', function (e) {
     e.stopPropagation();
     e.preventDefault();
});
obj.on('drop', function (e) {
     $(this).css('border', '2px dotted #0B85A1');
     e.preventDefault();
     var files = e.originalEvent.dataTransfer.files;
 
     //We need to send dropped files to firebase
     handleFileUpload(files,obj);
});
{% endhighlight %}

If the files are dropped outside the div, file is opened in the browser window. To avoid that we can prevent ‘drop’ event on document.

{% highlight javascript %}
$(document).on('dragenter', function (e) 
{
    e.stopPropagation();
    e.preventDefault();
});
$(document).on('dragover', function (e) 
{
  e.stopPropagation();
  e.preventDefault();
  obj.css('border', '2px dotted #0B85A1');
});
$(document).on('drop', function (e) 
{
    e.stopPropagation();
    e.preventDefault();
});
{% endhighlight %}

handle "Choose files" button

{% highlight javascript %}
// automatically submit the form on file select
$('#drop-zone-file').on('change', function (e) {
    var files = $('#drop-zone-file')[0].files;
    handleFileUpload(files, obj);
});
{% endhighlight %}

<strong>Step 4</strong> Create a function to handle Firebase Storage with callback

{% highlight javascript %}
function fireBaseImageUpload(parameters, callBackData) {

    // expected parameters to start storage upload
    var file = parameters.file;
    var path = parameters.path;
    var name;
    
    //just some error check 
    if (!file) { callBackData({error: 'file required to interact with Firebase storage'}); }
    if (!path) { callBackData({error: 'Node name required to interact with Firebase storage'}); }
    
    var metaData = {'contentType': file.type};
    var arr = file.name.split('.');
    var fileSize = formatBytes(file.size); // get clean file size (function below)
    var fileType = file.type;
    var n = file.name;
    
    // generate random string to identify each upload instance  
    name = generateRandomString(12); //(location function below)

    //var fullPath = path + '/' + name + '.' + arr.slice(-1)[0];
    var fullPath = path + '/' + file.name;

    var uploadFile = storageRef.child(fullPath).put(file, metaData);

    // first instance identifier
    callBackData({id: name, fileSize: fileSize, fileType: fileType, fileName: n});

    uploadFile.on('state_changed', function (snapshot) {
        var progress = (snapshot.bytesTransferred / snapshot.totalBytes) * 100;
        progress = Math.floor(progress);
        callBackData({
             progress: progress,
             element: name, 
             fileSize: fileSize, 
             fileType: fileType, 
             fileName: n});
    }, function (error) {
        callBackData({error: error});
    }, function () {
        var downloadURL = uploadFile.snapshot.downloadURL;
        callBackData({
              downloadURL: downloadURL, 
              element: name, 
              fileSize: fileSize, 
              fileType: fileType, 
              fileName: n});
    });
}

// function to generate random string to use in what creating firebase storage instance 
function generateRandomString(length) {
    var chars = "abcdefghijklmnopqrstuvwxyz";
    var pass = "";
    for (var x = 0; x < length; x++) {
        var i = Math.floor(Math.random() * chars.length);
        pass += chars.charAt(i);
    }
    return pass;
}

function formatBytes(bytes, decimals) {
    if (bytes == 0) return '0 Byte';
    var k = 1000;
    var dm = decimals + 1 || 3;
    var sizes = ['Bytes', 'KB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB'];
    var i = Math.floor(Math.log(bytes) / Math.log(k));
    return parseFloat((bytes / Math.pow(k, i)).toFixed(dm)) + ' ' + sizes[i];
}
{% endhighlight %}

<strong>Step 5</strong> Set up Firebase Storage & Initialize Firebase config

[Add and configure the Firebase SDK](https://firebase.google.com/docs/web/setup)

You must add your bucket to your Firebase SDK configuration.

{% highlight javascript %}
  // Set the configuration for your app
  // TODO: Replace with your project's config object
  var config = {
    apiKey: '<your-api-key>',
    authDomain: '<your-auth-domain>',
    databaseURL: '<your-database-url>',
    storageBucket: '<your-storage-bucket>'
  };
  firebase.initializeApp(config);

  // Get a reference to the storage service, which is used to create references in your storage bucket
  var storageRef = firebase.storage().ref();
{% endhighlight %}

<strong>Step 6</strong> Handle upload

Read the file contents using HTML5 FormData() when the files are dropped.

{% highlight javascript %}
function handleFileUpload(files, obj) {
    for (var i = 0; i < files.length; i++) {
        var fd = new FormData();
        fd.append('file', files[i]);

        console.log(files[i]);
        fireBaseImageUpload({
            'file': files[i],
            'path': '/file' //path_to_where_you_to_store_the_file
        }, function (data) {
            //console.log(data);
            if (!data.error) {
                if (data.progress) {
                    // progress update to view here
                }
                if (data.downloadURL) {
                    // update done
                    // download URL here "data.downloadURL"
                }
            } else {
                console.log(data.error + ' Firebase image upload error');
            }
        });
    }
};
{% endhighlight %}

<strong>Putting All together</strong> full Example

{% highlight html %}
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- The above 3 meta tags *must* come first in the head; any other head content must come *after* these tags -->
    <title>Bootstrap 101 Template</title>

    <!-- Bootstrap -->
    <link href="css/bootstrap.min.css" rel="stylesheet">

    <!-- HTML5 shim and Respond.js for IE8 support of HTML5 elements and media queries -->
    <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
    <!--[if lt IE 9]>
      <script src="https://oss.maxcdn.com/html5shiv/3.7.3/html5shiv.min.js"></script>
      <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
    <![endif]-->
    
    <style>
        #dragandrophandler {
            border: 2px dotted #0B85A1;
            width: 400px;
            color: #92AAB0;
            text-align: left;
            vertical-align: middle;
            padding: 10px 10px 10px 10px;
            margin-bottom: 10px;
            font-size: 200%;
        }
    
        #drop-zone {
            width: 360px;
            height: 240px;
            text-align: center;
            padding: 86px 0 0;
            outline: 2px dashed #92b0b3;
            outline-offset: -10px;
            -webkit-transition: outline-offset .15s ease-in-out, background-color .15s linear;
            transition: outline-offset .15s ease-in-out, background-color .15s linear;
            font-size: 1.25rem;
            background-color: #c8dadf;
            /* position: relative; */
            /* padding: 100px 20px; */
        }
    
        .btn-file input[type=file] {
            position: absolute;
            left: 0;
            top: 0;
            height: 100%;
            width: 100%;
            opacity: 0;
            cursor: pointer;
        }
    
        input[type=file] {
            display: block;
        }
    
        #drop-zone .drop-zone-caption {
            font-size: 20px;
            font-weight: 600;
            color: #919fa9;
            margin: 0 0 14px;
        }
    
        .btn.btn-primary {
            background-color: #00a8ff;
            border-color: #00a8ff;
        }
    </style>
    
  </head>
  <body>
    
    <form class="box" method="post" action="" enctype="multipart/form-data">
        <div id="drop-zone">
            <div class="drop-zone-caption">Drag & Drop Files Here</div>
            <span class="btn btn-primary btn-file" style="position: relative">
                <span>Choose files</span>
                <input type="file"id="drop-zone-file" name="files[]" multiple>
            </span>
        </div>
    </form>


    <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
    <!-- Include all compiled plugins (below), or include individual files as needed -->
    <script src="js/bootstrap.min.js"></script>
    
    <script>
    
        var obj = $("#drop-zone");
        obj.on('dragenter', function (e) {
            e.stopPropagation();
            e.preventDefault();
            $(this).css('border', '2px solid #0B85A1');
        });
        obj.on('dragover', function (e) {
            e.stopPropagation();
            e.preventDefault();
        });
        obj.on('drop', function (e) {
    
            $(this).css('border', '2px dotted #0B85A1');
            e.preventDefault();
            var files = e.originalEvent.dataTransfer.files;
    
            //We need to send dropped files to Server
            handleFileUpload(files, obj);
        });
    
        $(document).on('dragenter', function (e) {
            e.stopPropagation();
            e.preventDefault();
        });
        $(document).on('dragover', function (e) {
            e.stopPropagation();
            e.preventDefault();
            obj.css('border', '2px dotted #0B85A1');
        });
        $(document).on('drop', function (e) {
            e.stopPropagation();
            e.preventDefault();
        });
    
        // automatically submit the form on file select
        $('#drop-zone-file').on('change', function (e) {
            var files = $('#drop-zone-file')[0].files;
            handleFileUpload(files, obj);
        });
    
        function handleFileUpload(files, obj) {
            for (var i = 0; i < files.length; i++) {
                var fd = new FormData();
                fd.append('file', files[i]);
    
                console.log(files[i]);
                fireBaseImageUpload({
                    'file': files[i],
                    'path': 'path_to_where_you_to_store_the_file'
                }, function (data) {
                    //console.log(data);
                    if (!data.error) {
                        if (data.progress) {
                            // progress update to view here
                        }
                        if (data.downloadURL) {
                            // update done
                            // download URL here "data.downloadURL"
                        }
                    } else {
                        console.log(data.error + ' Firebase image upload error');
                    }
                });
            }
        };
    
        function fireBaseImageUpload(parameters, callBackData) {
    
            // expected parameters to start storage upload
            var file = parameters.file;
            var path = parameters.path;
            var name;
    
            //just some error check
            if (!file) { callBackData({error: 'file required to interact with Firebase storage'}); }
            if (!path) { callBackData({error: 'Node name required to interact with Firebase storage'}); }
    
            var metaData = {'contentType': file.type};
            var arr = file.name.split('.');
            var fileSize = formatBytes(file.size); // get clean file size (function below)
            var fileType = file.type;
            var n = file.name;
    
            // generate random string to identify each upload instance
            name = generateRandomString(12); //(location function below)
    
            //var fullPath = path + '/' + name + '.' + arr.slice(-1)[0];
            var fullPath = path + '/' + file.name;
    
            var uploadFile = storageRef.child(fullPath).put(file, metaData);
    
            // first instance identifier
            callBackData({id: name, fileSize: fileSize, fileType: fileType, fileName: n});
    
            uploadFile.on('state_changed', function (snapshot) {
                var progress = (snapshot.bytesTransferred / snapshot.totalBytes) * 100;
                progress = Math.floor(progress);
                callBackData({
                    progress: progress,
                    element: name,
                    fileSize: fileSize,
                    fileType: fileType,
                    fileName: n});
            }, function (error) {
                callBackData({error: error});
            }, function () {
                var downloadURL = uploadFile.snapshot.downloadURL;
                callBackData({
                    downloadURL: downloadURL,
                    element: name,
                    fileSize: fileSize,
                    fileType: fileType,
                    fileName: n});
            });
        }
    
        function generateRandomString(length) {
            var chars = "abcdefghijklmnopqrstuvwxyz";
            var pass = "";
            for (var x = 0; x < length; x++) {
                var i = Math.floor(Math.random() * chars.length);
                pass += chars.charAt(i);
            }
            return pass;
        }
    
        function formatBytes(bytes, decimals) {
            if (bytes == 0) return '0 Byte';
            var k = 1000;
            var dm = decimals + 1 || 3;
            var sizes = ['Bytes', 'KB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB'];
            var i = Math.floor(Math.log(bytes) / Math.log(k));
            return parseFloat((bytes / Math.pow(k, i)).toFixed(dm)) + ' ' + sizes[i];
        }
    
    </script>
  </body>
</html>
{% endhighlight %}



