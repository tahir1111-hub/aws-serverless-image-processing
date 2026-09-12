import boto3
from PIL import Image
from urllib.parse import unquote_plus
import os

s3 = boto3.client("s3")


def lambda_handler(event, context):

    # S3 event se bucket aur filename lena
    record = event["Records"][0]

    bucket = record["s3"]["bucket"]["name"]
    input_key = unquote_plus(record["s3"]["object"]["key"])

    print(f"Received image: {input_key}")

    # Sirf input1 folder ki images process karo
    if not input_key.startswith("input1/"):
        print("Not an input1 image. Skipping.")

        return {
            "statusCode": 200,
            "body": "Skipped"
        }

    # Temporary input file
    input_file = "/tmp/input.jpg"

    # S3 se image download
    s3.download_file(
        bucket,
        input_key,
        input_file
    )

    # Image open karo
    image = Image.open(input_file)

    # JPEG ke liye RGB me convert
    image = image.convert("RGB")

    # Original filename
    filename = os.path.basename(input_key)

    # Extension remove
    name = os.path.splitext(filename)[0]

    # 3 different sizes
    sizes = {
        "small": (200, 200),
        "medium": (500, 500),
        "large": (1000, 1000)
    }

    # 3 images create karo
    for size_name, size in sizes.items():

        # Original image ki copy
        output_image = image.copy()

        # Resize while maintaining aspect ratio
        output_image.thumbnail(size)

        # Temporary output file
        output_file = f"/tmp/{name}_{size_name}.jpg"

        # JPEG me save
        output_image.save(
            output_file,
            format="JPEG",
            quality=85
        )

        # S3 output2 folder
        output_key = f"output2/{name}_{size_name}.jpg"

        # S3 me upload
        s3.upload_file(
            output_file,
            bucket,
            output_key,
            ExtraArgs={
                "ContentType": "image/jpeg"
            }
        )

        print(f"Created: {output_key}")

    return {
        "statusCode": 200,
        "body": "3 images created successfully"
    }
