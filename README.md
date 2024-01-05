# Animate

A local video animator using Replicate and stable-video-diffusion. Non-commercial, research only usage.

## Prerequisites

1. Make a [Replicate](https://replicate.com) account and set [your token](https://replicate.com/account/api-tokens):

   ```sh
   export REPLICATE_API_TOKEN=<token>
   ```

## Usage

1. Install the required packages from `requirements.txt` using pip:

   ```sh
   pip install -r requirements.txt
   ```

2. Make the script `animate` executable:

   ```sh
   chmod u+x animate
   ```

3. You can run the script directly using the following command:

   ```sh
   ./animate path_to_your_image.png
   ```

   This will animate the image at the specified path using the default parameters.

4. Optionally, you can add the script to your PATH to run it from anywhere. To make this change persistent across sessions, add the export command to your shell's configuration file (e.g., `~/.bashrc` or `~/.bash_profile` for bash, `~/.zshrc` for zsh):

   ```sh
   echo 'export PATH=$PATH:/path/to/script/directory' >> ~/.bashrc
   ```

   Then, source your shell's configuration file to apply the change immediately:

   ```sh
   source ~/.bashrc
   ```

5. You can also add this as a Finder quick action, using the following AppleScript:

   ```applescript
   on run {input, parameters}
       repeat with aFile in input
           set file_path to POSIX path of (aFile as alias)
           do shell script "export REPLICATE_API_TOKEN=<your_token>; /path/to/python /path/to/animate " & quoted form of file_path
       end repeat
       return input
   end run
   ```

You can also specify additional parameters such as `video_length`, `sizing_strategy`, `frames_per_second`, `motion_bucket_id`, `cond_aug`, `decoding_t`, and `seed`. For example:

```sh
./animate path_to_your_image.png --video_length 14_frames_with_svd --sizing_strategy maintain_aspect_ratio
```

This will animate the image with a video length of 14 frames with SVD and a sizing strategy of maintaining aspect ratio.

The animated video will be saved in the same directory as the original image with `-animated` appended to the original file name.

## Options

Option|Type|Default|Description|
---|---|---|---|
`input_image`|str|None|The path to the image to animate|
`video_length`|str|"14_frames_with_svd"|Length of the generated video|
`sizing_strategy`|str|"maintain_aspect_ratio"|Strategy for sizing the output video|
`frames_per_second`|int|6|Frames per second in the generated video|
`motion_bucket_id`|int|27|Increase overall motion in the generated video|
`cond_aug`|float|0.02|Amount of noise to add to input image|
`decoding_t`|int|14|Decoding time|
`seed`|int|None|Seed for random number generator|
`output_file_path`|str|None|The path where the animated video will be saved. If not specified, the animated video will be saved in the same directory as the original image with `-animated` appended to the original file name|
