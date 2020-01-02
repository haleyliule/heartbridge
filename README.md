# iOS Heart Rate Data Export

Combined with an Apple Watch, the iOS Health app contains a wealth of heart rate readings. I always found these readings a little difficult to play with in the Health app, and couldn't find a way to easily export them to a format I could manipulate/visualize the readings using (like a JSON or CSV file).

Fortunately with the [Shortcuts](https://apps.apple.com/us/app/shortcuts/id915249334) app, accessing this data is a lot easier. This combines a shortcut with a quick API endpoint (using [Flask](http://flask.palletsprojects.com/en/1.1.x/)) to capture and store the data the shortcut exports. 

This Python script can receive data from Shortcuts, automatically export it to the directory of your choosing (in CSV or JSON format) and automatically name files according to what date range it covers. Exported files contain a time stamp ("Start Date" in Health) and heart rate ("Value" in Health).

**Note**: This is designed to be run on your local computer! It wasn't made to be deployed to a server (yet).

## Requirements

You will need two things:

* A computer with Python (>=3.5) installed
* An iPhone with [Shortcuts](https://apps.apple.com/us/app/shortcuts/id915249334) installed

On the first run, the shortcut will prompt for access to your Health data (particularly heart rate data).

## Getting Started

1. Clone this repository to your computer, and install required packages by opening up a terminal and typing the following:

```bash
git clone https://github.com/mm/heartbridge.git && cd heartbridge
pip install -r requirements.txt
```

2. Afterwards, run `app.py`, specifying where you want export files stored and in what format you want them exported to (JSON/CSV). For example, this command:

```bash
python3 app.py --directory ~/Desktop --type csv
```

... will save all exported files to the desktop in CSV format. If no arguments are specified, the script will output files in CSV format to the current working directory. Please make sure the folder exists before running the script.

3. Make note of the endpoint URL the script prints out, and ensure the script is allowed to accept incoming connections if your firewall prompts you. In this case, mine would be ```http://matt-mac-mini.local:5000/heartrate```:

![The line of terminal output "Now accepting POST requests at http://matt-mac-mini.local:5000/heartrate" tells me that my endpoint URL is http://matt-mac-mini.local:5000/heartrate](img/endpoint-image.png)

4. On your iPhone, [download the shortcut to extract Health samples](https://www.icloud.com/shortcuts/2d24033f74bb493c8017e4986e6233bf). It will ask you what the REST endpoint URL you just noted is.

5. Run the shortcut! You will be prompted to select the date range you want to cover. The end date of the date range you specify is not included in the data returned. For example, to get all data for January 1st, 2020:

![To select all data for January 1st, 2020, you would select a date range between January 1st and 2nd](img/shortcut-iPhone.png)

The script will output information about the data it receives from the shortcut to the console:

![Information about the data received by the script (number of samples and path of the file produced) is outputted to the console](img/script-output.png)

6. Stop running the script whenever you're finished exporting all the data you need. Enjoy exploring your heart rate data!