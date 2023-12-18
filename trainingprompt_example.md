# AI Training Prompt Example

# User Prompt

**system**:
(Personal system prompt removed for privacy.)

--------------------

**user**:
(Prompt removed for brevity, see "trainingprompt.md" for text.)

--------------------
# GPT-4 Response

**assistant**:
Understood. I've loaded the syntax specification for Thing-Action-Context Language (TACL) into context. I'm ready to assist with converting code into TACL form whenever you're ready to proceed.

--------------------
# User Prompt

**user**:
"morningpod.py"
```python
from bs4 import BeautifulSoup
from datetime import datetime
import os
import requests
import subprocess
from sys import platform 
import time
import vlc

def download_latest_weather_podcast(feed_url):
    response = requests.get(feed_url)
    response.raise_for_status() # will raise an HTTPError if the HTTP request returned an unsuccessful status code
    
    # Parse the feed using BeautifulSoup
    soup = BeautifulSoup(response.content, features='xml')
    # Find the first <item> node
    first_item = soup.find('item')
    # Get the URL of the first enclosure in the first <item>
    audio_url = first_item.find('enclosure')['url']
    
    # Download the audio file
    audio_response = requests.get(audio_url)
    audio_response.raise_for_status()
    
    # Generate a file name based on the current date and time
    file_name = f"weather_podcast_{datetime.now().strftime('%Y%m%d%H%M%S')}.mp3"
    
    # Save the file
    with open(file_name, 'wb') as file:
        file.write(audio_response.content)
    
    return file_name

def play_audio_file(file_name):
    # Define a VLC instance
    player = vlc.MediaPlayer(file_name)
    
    # Play the audio file
    player.play()
    # Wait for the audio to play
    time.sleep(1) # Give player time to start
    duration = player.get_length() / 1000 # Get the duration in seconds
    time.sleep(duration) # Wait for the file to finish playing

def print_text_document(file_path):
    # Ensure the file exists to avoid errors
    if os.path.exists(file_path):
        # Command to print the document
        command = f'notepad /p "{file_path}"'
        os.system(command)
    else:
        print(f"The file {file_path} does not exist.")

def print_text_document2(file_path):
    # Check the OS
    if platform == "win32":
        # Windows command
        command = ["notepad", "/p", file_path]
    elif platform == "linux":
        # Linux command (you may need to change 'lp' to another command depending on your setup)
        command = ["lp", file_path]
    elif platform == "darwin":
        # macOS command
        command = ["lp", file_path]
    else:
        print("Unsupported operating system.")
        return
    
    # Run the command
    try:
        subprocess.run(command, check=True)
    except subprocess.CalledProcessError as e:
        print(f"An error occurred while trying to print the document: {e}")

def main():
    feed_url = 'https://feed.pod.co/usa-weather-today'
    
    # Download the latest weather podcast
    print("Downloading today's weather podcast...")
    audio_file = download_latest_weather_podcast(feed_url)
    
    # Play the downloaded weather podcast
    print("Playing today's weather podcast...")
    play_audio_file(audio_file)

    # Cleanup: delete the audio file after playing
    os.remove(audio_file)

    # Print the daily form
    print("Printing Today's Form...")
    print_text_document('morningpod.txt')

    
    print("Morning routine completed.")

if __name__ == "__main__":
    main()

```

--------------------
# GPT-4 Response

**assistant**:
```TACL
<Main>[DefineAction]{
    <Input> is {}
    <Default><Error>"An Error has occurred."
    <Body>{
        <FeedUrl>"https://feed.pod.co/usa-weather-today"

        # Download the latest weather podcast
        [Print]{"Downloading today's weather podcast..."}
        <AudioFile>[DownloadLatestWeatherPodcast]{FeedUrl}

        # Play the downloaded weather podcast
        [Print]{"Playing today's weather podcast..."}
        [PlayAudioFile]{AudioFile}

        # Cleanup: delete the audio file after playing
        [RemoveFile]{AudioFile}

        # Print the daily form
        [Print]{"Printing Today's Form..."}
        [PrintTextDocument]{"morningpod.txt"}

        [Print]{"Morning routine completed."}
    }
}

<DownloadLatestWeatherPodcast>[DefineAction]{
    <Input>{FeedUrl},
    <Default><Error>"An Error occurred during podcast download."
    <Body>{
        <Response>[GetRequest]{FeedUrl}
        [RaiseForStatus]{Response}
        <Soup>[ParseWithBeautifulSoup]{Response.content, "xml"}
        <FirstItem>[Soup.find]{"item"}
        <AudioUrl>[FirstItem.find]{"enclosure"}["url"]
        <AudioResponse>[GetRequest]{AudioUrl}
        [RaiseForStatus]{AudioResponse}
        <FileName>[FormatString]{"weather_podcast_%s.mp3", [CurrentDateTime]{"%Y%m%d%H%M%S"}}
        [WriteToFile]{FileName, AudioResponse.content}
        <Return>{FileName}
    }
}

<PlayAudioFile>[DefineAction]{
    <Input>{FileName},
    <Default><Error>"An Error occurred while playing the audio file."
    <Body>{
        <Player>[CreateVLCMediaPlayer]{FileName}
        [Player.play]
        [Sleep]{1}
        <Duration>[Player.get_length] / 1000
        [Sleep]{Duration}
    }
}

<PrintTextDocument>[DefineAction]{
    <Input>{FilePath},
    <Default><Error>"An Error occurred while printing the document."
    <Body>{
        [If]{
            (c)[FileExists]{FilePath},
            (t)<Command>[FormatString]{"notepad /p \"%s\"", FilePath},
            (f)[Print]{[FormatString]{"The file %s does not exist.", FilePath}}
        }
        [SystemCommand]{Command}
    }
}

<PrintTextDocument2>[DefineAction]{
    <Input>{FilePath},
    <Default>"Unsupported operating system."
    <Body>{
        [If]{
            (c)[Equals]{[Platform], "win32"},
            (t)<Command> is ["notepad", "/p", FilePath],
            (f)[If]{
                (c)[Equals]{[Platform], "linux"},
                (t)<Command> is ["lp", FilePath],
                (f)[If]{
                    (c)[Equals]{[Platform], "darwin"},
                    (t)<Command> is ["lp", FilePath],
                    (f)[Print]{"Unsupported operating system."}
                }
            }
        }
        [Attempt]{
            [SubprocessRun]{Command, True},
            [Print]{[FormatString]{"An error occurred while trying to print the document: %s", [Error]}}
        }
    }
}

[RemoveFile][DefineAction]{
    <Input>{FileName},
    <Default><Error>"An Error occurred while removing the file."
    <Body>{
        [OsRemove]{FileName}
    }
}

[Main]
```

Please note that for actions such as `GetRequest`, `RaiseForStatus`, `ParseWithBeautifulSoup`, `FormatString`, `CurrentDateTime`, `WriteToFile`, `CreateVLCMediaPlayer`, `Sleep`, `SubprocessRun`, `FileExists`, `SystemCommand`, and `OsRemove`, you would need to define these with the appropriate functionality as they correspond to the Python's requests, os, subprocess, datetime, and vlc library functions and classes. Also, the handling of attributes in TACL, such as `["url"]` and `["content"]`, needs to be adapted to match the TACL's way of accessing properties or elements.