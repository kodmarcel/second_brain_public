---  
share: true  
tag: public  
---  
# Running as service  
  
    place below text in /etc/systemd/system/scraping-api-server.service and edit it according to needs  
  
    [Unit]  
        Description=ScrapingAPIServer  
        Documentation=https://github.com/mediabiz-dev/scraping-server-api  
        After=network.target  
  
    [Service]  
        ExecStart=/home/mediabiz/scraping-server-api/server_service.sh  
        Restart=always  
        RestartSec=10s  
        LimitCORE=infinity  
  
    [Install]  
        WantedBy=multi-user.target  
    ~                                                                                                                                                                                                                                         DO not forget to make sure server_srvice.sh has to be executable.                                                           
  
    and run following commands  
  
    sudo systemctl daemon-reload  
    sudo systemctl enable scraping-api-server #to start on boot  
    sudo systemctl start scraping-api-server  
    sudo systemctl status scraping-api-server  #to check if it's running and everything is ok  
  
    to check logs use  
  
    journalctl -e -u scraping-api-server  
  
  
