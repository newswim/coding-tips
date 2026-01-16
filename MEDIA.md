# Media Optimization

## Setup

```bash
brew install ffmpeg
```

## FFmpeg (and working with GIF files)

### Convert GIF to MP4 (universal compatibility)

```bash
ffmpeg -i input.gif -c:v libx264 -pix_fmt yuv420p -vf "scale=1392:-2" -crf 23 -an output.mp4
```

`-crf 23` controls quality (lower = better), `-pix_fmt yuv420p` ensures Mac/iPhone compatibility.

### Convert GIF to WebM (smallest size)

```bash
ffmpeg -i input.gif -c:v libvpx-vp9 -b:v 0 -crf 30 -vf "scale=1392:-2" -an output.webm
```

Requires libvpx support. Best for Chrome/Firefox.

### Extract first frame as poster image

```bash
ffmpeg -i video.mp4 -frames:v 1 -q:v 2 -update 1 poster.jpg
```

### Compress PNG to JPG

```bash
ffmpeg -i screenshot.png -vf "scale=1392:-1" -q:v 4 compressed.jpg
```

## HTML Video Embed

Prioritizes WebM for modern browsers, falls back to MP4 for Safari/iOS.

```html
<video
  autoplay
  loop
  muted
  playsinline
  width="1392"
  poster="poster.jpg"
  style="max-width: 100%; height: auto;"
>
  <source src="output.webm" type="video/webm" />
  <source src="output.mp4" type="video/mp4" />
  <img src="poster.jpg" alt="Description of animation" />
</video>
```
