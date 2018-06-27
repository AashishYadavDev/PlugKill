# PlugKill
WordPress Plugin Security Scanner
## Tutorial
1. Start downloading and analysing WordPress plugins:
`python plugkill.py -p`
2. Take the output from `wpscan` and analyse all the themes and plugins that it identified.

    First collect the scan in a file, wpscan.log:

    `wpscan http://yourtargetsite.com | tee wpscan.log`

    then
    `python plugkill.py -w wpscan.log`

3. Just analyse a folder already on disk, reporting only severity 1 issues (critical such as RCE, SQLi):

    `python plugkill.py -a /var/www -s 1`
    ## Usage

```
usage: plugkill.py [-h] [-d PLUGINDIR] [-o OUTPUTDIR] [-l LOGFILE] [-L]
                    [-w WPSCAN] [-p] [-n] [-a ANALYSE] [-b] [-s {1,2,3,4}]
                    [--debug DEBUG]

Grab the most popular wordpress plugins, unpack them and look for dangerous
code use

optional arguments:
  -h, --help            show this help message and exit
  -d PLUGINDIR, --plugindir PLUGINDIR
                        Base URL for scraping plugins
  -o OUTPUTDIR, --outputdir OUTPUTDIR
                        Output dir for saving downloaded files
  -l LOGFILE, --logfile LOGFILE
                        Log file to write to
  -L, --nologfile       Disable writing a log file
  -w WPSCAN, --wpscan WPSCAN
                        Download all plugins mentioned in the supplied output
                        file from wpscan
  -p, --plugins         WordPress plugins mode. Scrape and analyse all top
                        plugins on wordpress.org/plugins
  -n, --nodownload      Don't do any scraping, just analyse any code already
                        present
  -a ANALYSE, --analyse ANALYSE
                        Just analyse a folder without doing anything else
  -b, --binaries        Search within binary files as if they were text
  -s {1,2,3,4}, --severity {1,2,3,4}
                        Report only issues of this severity level and up
                        (1=critical, 4=medium)
  --debug DEBUG         Output search commands
```
