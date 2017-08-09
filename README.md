# weatTrip
first program in tf , thanks hy


1. 图片裁切 cropper https://github.com/fengyuanchen/cropper
    裁切过程是 先将图片用ajax传递给后端 传递给后端的 图片是blob格式， 将后端返回的数据填充到页面上。
      // $('#init-img').cropper('clear');
      // 裁切后得到的图片
      
      // $('#init-img') 放置要裁切图片的img的id
      completeImg = $('#init-img').cropper("getCroppedCanvas");
      // console.log('completeImg', completeImg);
      // 调用ajax将cropped的图片传给后台 在拿到后台返回的数据填写到头像上
      completeImg.toBlob(function(blob){
        // ============================================================================
        // console.log(completeImg.filesize, '图片大小');
        // console.log(blob, '------------');
        var fm = new FormData();
        fm.append('file',blob);
        var xhr = new XMLHttpRequest();
        xhr.open('post','http://' + ajaxPre + '/uploadImage',true);
        xhr.onreadystatechange = function(){
          if(this.readyState == 4){
              // console.log(JSON.parse(this.responseText), '========');
              var data = JSON.parse(this.responseText);
              var url = data.data.arrdata[0].url;
              if(data.message === '上传成功') {
                if(btnType == 1) {
                  $('.self-show').attr('src', imgPre + url);
                  // console.log( $('.self-show').attr('src'), 'src');
                  $('#init-img').cropper('clear');
                  // $('.body-content').append($imgTip);
                  // var left = window.innerWidth;
                  // $('.img-tip').addClass('img-tip-success');
                  // var _left = (left - $('.img-tip-success').width())/2;
                  // $('.img-tip').css('top', 200 + 'px').css('left', $(document).scrollLeft() + _left + 'px').hide(300);
                  $('.body-content .modify-avatar-model').remove();
                  $('.mask').hide();
                } else {
                  $('.self-avatar').attr('src', imgPre + url);
                  // console.log( $('.self-avatar').attr('src'), 'avatar src');
                  $('#init-img').cropper('clear');
                  $('.body-content .modify-avatar-model').remove();
                  $('.mask').hide();
                }
              }
          }
        }
        xhr.send(fm);
        // ============================================================================
      });
      
      
      // 上传图片
      function getObjectURL(file) {
        // var url = null;
        // var url = window.readAsDataUrl(file);
        if (window.createObjectURL != undefined) { // basic
            url = window.createObjectURL(file);
        } else if (window.URL != undefined) { // mozilla(firefox)
            url = window.URL.createObjectURL(file);
        } else if (window.webkitURL != undefined) { // webkit or chrome
            url = window.webkitURL.createObjectURL(file);
        }
        return url;
      }
      
2. 
