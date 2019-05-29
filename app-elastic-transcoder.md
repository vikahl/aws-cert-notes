# Elastic transcoder

- Media transcoder, converts media files from source format into other formats
- Provides presets for popular output formats
- Pay per transcoded minute and output resolution

## Example of usage

1. Files are uploaded to a S3 bucket (i.e. with file upload from website)
2. A lambda function is triggered which will read metadata and send it to elastic transcoder
3. The elastic transcoder transcodes the video to multiple formats/resolution for different devices
4. The transcoded files are uploaded to S3
