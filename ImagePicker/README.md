# 图片选择（相机+相册+裁剪）

图片选择（相机+相册+裁剪），改自 [ImagePicker](https://github.com/linchaolong/ImagePicker) 及 [Android-Image-Cropper](https://github.com/ArthurHub/Android-Image-Cropper)

## 简单用法

```java
public class ImagePickerActivity extends FragmentActivity {
    private final PickCallback cropCallback = new PickCallback() {
        @Override
        public void onPermissionDenied(String[] permissions, String message) {
            Toast.makeText(ImagePickerActivity.this, message, Toast.LENGTH_SHORT).show();
        }

        @Override
        public void cropConfig(ActivityBuilder builder) {
            builder.setMultiTouchEnabled(true)
                    .setGuidelines(CropImageView.Guidelines.ON_TOUCH)
                    .setCropShape(CropImageView.CropShape.OVAL)
                    .setRequestedSize(400, 400)
                    .setFixAspectRatio(true)
                    .setAspectRatio(1, 1);
        }

        @Override
        public void onCropImage(@Nullable Uri imageUri) {
            Toast.makeText(ImagePickerActivity.this, String.valueOf(imageUri), Toast.LENGTH_SHORT).show();
        }
    };

    public void onCamera(View view) {
        ImagePicker.getInstance().startCamera(this, true, cropCallback);
    }

    public void onGallery(View view) {
        ImagePicker.getInstance().startGallery(this, true, cropCallback);
    }

    @Override
    protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        ImagePicker.getInstance().onActivityResult(this, requestCode, resultCode, data);
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        ImagePicker.getInstance().onRequestPermissionsResult(this, requestCode, permissions, grantResults);
    }

}
```