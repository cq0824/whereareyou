# whereareyou
Inspired by [whereami](https://github.com/kootenpv/whereami). Passive indoor localization using the Wifi signal strength of a users devices. A set of slaves (like Raspberry Pis) is distributed at the location and send the signal strengths of detected devices to a master server. Based on a pretrained model the master predicts where the devices currently are located.

## Setup

- Install Cython  
`apt-get install cython`
- Install Python dependencies  
`pip install -r requirements.txt`

### Slaves
- Install aircrack-ng  
`apt-get install aircrack-ng`  


### Master  
- Copy `example.env` to `.env` and add the appropriate configuration keys  
`cp example.env .env`
- Adapt `static/office.svg` and `static/office_mapping.json` to your office (we recommend [this](http://editor.method.ac/) online editor). You can test your office mapping at /test_mapping.
- Create the database initially  
`python -c "from master import db, load_locations; db.create_all(); load_locations()"`  


## Usage
### Slaves
- Copy `example.run.sh` to `run.sh` and adapt the configuration to your needs  
`cp example.run.sh run.sh`  
  * FLOW_TOKEN - token for the Flowdock channel that should receive notifications when the slave crashes
  * SLAVE_ID - unique identifier of the slave
  * INTERFACE - Wifi interface that can be set to monitor mode
  * NETWORK - Wifi network monitored people should be logged in to
  * MASTER_ADDRESS - Internal IP address of the master server
- Run `bash run.sh` on every slave device

### Master
- Run `master.py` on a device that can be accessed by the slaves in your internal network  
`python master`  
