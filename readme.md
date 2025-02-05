# Requirements
Windows 10 and up  
4 Go RAM minimum


# Pre-built package usage
- Pre-built archive can be downloaded from the Release section
- Unzip the .rar file anywhere  
- Launch the .exe  
- Use the 'Browse' buttons to specify input audio file (.wav, .mp3 extension tested, could work with others)  
- Optionnaly choose an output directory (will be created if it doesn't exist)


### Python script usage
- TODO : A python environment will be created to install the requirements. They need to be installed manually for now...  
- script is executed using the following command from any console, once the requirements are installed :  

```bash
~simpleTranscriber$ python main.py
```

### Building a standalone executable from sources :
- The models needs to be downloaded using the commented line (main.py:L89) :
```python
model = whisper.load_model("small")
```
- Alternatively, it is contained in the pre-build package in the .rar archive on the drive (CF link above)

Change USERNAME with actual UserName and potentially adapt paths/python version to fit your install locations.  

```bash
pyinstaller main.py --name exeFile --add-data 'libs/ffmpeg/bin/ffmpeg.exe;libs/ffmpeg/bin' --add-data 'libs/ffmpeg/bin/ffprobe.exe;libs/ffmpeg/bin' --add-data 'libs/ffmpeg/bin/ffplay.exe;libs/ffmpeg/bin' --add-data 'C:/Users/USERNAME/.cache/whisper/small.pt;models' --add-data 'C:/Users/USERNAME/AppData/Local/Programs/Python/Python312/Lib/site-packages/whisper/assets;whisper/assets'
```

This will produce a 'dist/' folder containing :  
.  
└── dist/  
    ├── _internal/  
    │   ├── ...  
    │   ├── models/  
    │   ├── libs/  
    │   └── ...  
    └── exeFile.exe  
  
Both 'models/' and 'libs/' directories need to be moved outside of the '_internal/' directory (and 'models' directory needs to be moved inside the 'libs' dir.) to obtain a final folder :  
.  
└── dist/  
    ├── _internal/  
    ├── libs/models/  
    └── exeFile.exe  


# Credits
Based on the OpenAI developped Whisper model (https://github.com/openai/whisper)  
Currently using an extension of it : whisper-timestamped (https://github.com/linto-ai/whisper-timestamped), for this project's purposes, the original Whisper model should be sufficient (TODO).
