## System requirements
You can install Siali Label on a Linux, Windows, or MacOSX machine running Python 3.6 or later.

### Port requirements
Siali Label expects port 8080 to be open by default. To use a different port, specify it when starting Siali Label. See [Start Siali Label](start.html). 

### Server requirements
Allocate disk space according to the amount of data you plan to label. As a benchmark, 1 million labeling tasks take up approximately 2.3GB on disk when using the SQLite database. 50GB of disk space is recommended for production instances. 

Use a minimum of **8GB RAM**, but 16GB RAM is recommended. for example, t3.large or t3.xlarge on Amazon AWS.

For more on using Siali Label at scale and labeling performance, see [Start Siali Label](start.html).

### Software requirements
PostgreSQL version 11.5 or SQLite version 3.35 or higher.