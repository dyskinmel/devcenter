---
title: Building with FAKE (F# Make)
menu:
  tutorials-main:
    weight: 20

---
To add support to your FAKE build scripts, open your app's [Workflow Editor on bitrise.io](/getting-started/manage-your-bitrise-workflow/)
and add a **Script** Step to your workflow.

Below you can find an example script content to perform a build with FAKE, make sure you FILL OUT THE PARAMETERS at the top of the script!

```bash
#!/bin/bash
set -ex

# Fill out these parameters:
# You should use the same directory that you set in your build script for the FAKE dll
output_directory=tools
fake_build_script=build.fsx
fake_target_name=
fake_option_flags=

# ---

fake_exe="${output_directory}/FAKE/tools/fake.exe"

if [ ! -f "${fake_exe}" ]; then
  printf "\e[34mInstalling FAKE\e[0m\n"
  nuget install FAKE -OutputDirectory "${output_directory}" -ExcludeVersion -NoCache -NonInteractive
fi

command=("mono" "${fake_exe}")

if [ -n "$fake_build_script" ] ; then
  command+=("${fake_build_script}")
fi

if [ -n "$fake_target_name" ] ; then
  command+=("${fake_target_name}")
fi

if [ -n "$fake_option_flags" ] ; then
  command+=("${fake_option_flags}")
fi

printf "\e[34mExecuting ${fake_build_script}\e[0m\n"
$(IFS=' '; echo "${command[*]}")
```

{% include message_box.html type="important" title="Don't forget!" content="

* You should update the `output_directory` and `fake_build_script` variables for your needs and you are ready to go!
* You should set the `output_directory` to the same directory where your build script will search for the FAKE dlls." %}

{% include banner.html banner_text="Add support for FAKE build scripts" url="https://app.bitrise.io/dashboard/builds" button_text="Go to your app" %}