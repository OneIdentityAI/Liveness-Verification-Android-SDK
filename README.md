# Liveness-Verification-SDK
One Identity Liveness Verification SDK
Includes the following aar file into your android studio project based on the following file structure inside the libs folder
```
Your Project Folder
            |
            |---- app
                     |
                     |----libs
                             |
                             |----liveness_verification.aar
```
In your build.gradle file, includes the following at the dependencies section
```
implementation fileTree(dir: 'libs', include: ['*.jar'])
```
The full sample as follow:
```
dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    implementation files('libs/liveness_verification.aar')
    implementation .....
}
```

In your fragment or activity, call the following function to trigger liveness activity
```
public int LIVENESS_REQUEST_CODE = 1; (You can eclare any request code)

Intent intent = new Intent(ProfileSelfieActivity.this, CameraActivity.class);
intent.putExtra("token", "Place your token here");
intent.putExtra("apikey", "Place your apikey here");
startActivityForResult(intent, LIVENESS_REQUEST_CODE);
```
In your activity,implement the following callback function
```
public void onActivityResult(int requestCode, int resultCode, Intent data) {
    if (requestCode == LIVENESS_REQUEST_CODE) {
        if (resultCode == RESULT_OK) {
            String returnedResult = data.getData().toString();
            Log.e("Result", returnedResult);
            try {
                JSONObject json = new JSONObject(returnedResult);
                String status = json.getString("status");
                String type = json.getString("type");
                String message = json.getString("message");
                String selfieImage = json.getString("selfie_image");

                //Perform your logic here
            } catch (Exception e) {

            }
        }
    }
}
```
Result will be as follow in json:
```
{
    "status": "200",
    "type": "ok",
    "message": "Liveness verification successful",
    "selfie_image": "a3e40f30-7659-11e9-bada-bf2c9bd03a26.png"
}
```
To view the uploaded file, refer to the following document to trigger the function by passing in file_name value into document_name
[1id API Document](https://doc.1id.ai/#operation/view-upload)
