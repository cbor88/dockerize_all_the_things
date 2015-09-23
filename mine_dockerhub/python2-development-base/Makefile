help:
	@echo -e " make clean 			- Deletes the *.pyc files"
	@echo -e " make tmux 			- Run a tmux session."
	@echo -e " make bash 			- Run a bash session."
	@echo -e " make notebook 		- Start the ipython notebook."
	@echo -e " make up 				- docker-compose up."
	@echo -e " make rm 				- docker-compose rm."
	@echo -e " make stop 			- docker-compose stop"
	@echo -e " make ps 				- docker-compose ps"
	@echo -e " make logs 			- View the app logs (logs/log.txt)."

clean:
	@echo -e "\nDeleting pyc files...\n";
	rm -fr `find . -name "*.pyc"`;
	@echo -e "\nDeleting pyc files...[DONE]\n";

tmux:
	@docker-compose run devpython2 tmux -2 new -s new-session

notebook:
	@docker-compose run devpython2 ipython notebook --no-browser --ip=0.0.0.0 --port 8888

up:  
	@docker-compose up -d 

rm:  
	@docker-compose rm

stop:  
	@docker-compose stop

ps:  
	@docker-compose ps

bash:  
	@docker-compose run devpython2 bash

log:  
	@tail -f logs/log.txt

