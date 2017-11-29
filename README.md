# bw_stats
bw_stats is a front-end webapp to visualize data gathered by it's own python
script from OpenWRT/LEDE library [wrtbwmon](https://github.com/pyrovski/wrtbwmon)

## How?
A properly configured wrtbwmon tool running on a router produces a usage.db file
that can be published by a symlink to the /www/ folder and can then be parsed by
an external tool.

bw_stats can be run on the router itself, therefore having no need to publish the
file but, in my case, I'm running bw_stats on a small headless server running on
an orange pi so the file needs to be fetched remotely.

By parsing the usage.db file (which is in fact a CSV file) every 5 seconds,
bw_stats builds a one month long database. The front-end app then uses this
database to show nice graphics using your bandwith-usage data.

## Why?
The actual tools and visualizations (wrtbwmon included) are very limited in
terms of information. The Luci visualization for wrtbwmon shows no graphs but
a improved version of the usage table that wrtbwmon itself provides, on the other
hand, tools like nlbwmon that actually have graphs have a better approach and
allow to select accounting period for them, but no tool/visualization includes
realtime bandwith usage graphs.

## Installation
After setting up wrtbwmon and scheduling the task to publish the usage every 5
seconds, just copy the latest release of bw_stats to your router or server
and make it available from any html server running within it.

Modify the db/log_usage.py file variables to set the stats.json and usage.db
locations.

Set the db/log_usage.py script to run on server boot, remember to run it on
second plane to don't hang up your server forever. The script loops itself so
you don't have to schedule a cron task for it.

## Usage
With everything set up, just point any browser to the url where bw_stats is
available and enjoy your cool graphs.
