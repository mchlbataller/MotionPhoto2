# MotionPhoto2 - Headless Version

This is a headless version of MotionPhoto2 that can be run in Docker containers without GUI dependencies.

## Changes Made

- Removed Gooey GUI dependency
- Converted to command-line only interface
- Added Docker support for containerized execution
- Removed all GUI-specific widgets and options

## Docker Usage

### Building the Image

```bash
docker build -t motionphoto2 .
```

### Running with Docker

#### Process a Directory
```bash
docker run -v /path/to/input:/input -v /path/to/output:/output motionphoto2 \
  python motionphoto2.py --input-directory /input --output-directory /output --verbose
```

#### Process Individual Files
```bash
docker run -v /path/to/files:/input -v /path/to/output:/output motionphoto2 \
  python motionphoto2.py --input-image /input/image.jpg --input-video /input/video.mp4 --output-directory /output
```

### Using Docker Compose

1. Create input and output directories:
```bash
mkdir input output
```

2. Place your files in the input directory

3. Run with docker-compose:
```bash
docker-compose up
```

4. Find processed files in the output directory

## Command Line Usage

All original command-line functionality remains intact:

```bash
# Process directory
python motionphoto2.py --input-directory /path/to/photos --output-directory /path/to/output

# Process individual files
python motionphoto2.py --input-image photo.jpg --input-video video.mp4

# With EXIF matching
python motionphoto2.py --input-directory /path/to/photos --exif-match --output-directory /path/to/output

# Recursive processing
python motionphoto2.py --input-directory /path/to/photos --recursive --output-directory /path/to/output
```

## Available Options

```
Process a Directory:
  --input-directory    Mux all the photos and videos in a directory
  --recursive          Recursively process subdirectories
  --exif-match         Match files by Live Photo metadata
  --incremental-mode   Skip photos already muxed in output
  --copy-unmuxed       Copy other files
  --output-directory   Directory where to save the resulting Motion Photos

Settings:
  --delete-video       Delete video after muxing
  --overwrite          Overwrite the original image
  --keep-temp          Keep muxing temp files
  --verbose            Verbose output

Process a Single File:
  --input-image        Input file image (.heic, .jpg)
  --input-video        Input file video (.mov, .mp4)
  --output-file        Output Live Photo filename
  --no-xmp             No XMP processing (just glue image and video using Samsung tags)
```

## Requirements

- Python 3.7+
- ExifTool
- lxml
- PyExifTool
- six

No GUI dependencies are required.