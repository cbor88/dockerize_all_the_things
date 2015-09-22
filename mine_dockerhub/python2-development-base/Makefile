help:
	@echo -e "\nHELP:\n"
	@echo -e " make clean \n\tDeletes the *.pyc files\n\n"
	@echo -e " make tmux \n\tRun a tmux session.\n\n"

clean:
	@echo -e "\nDeleting pyc files...\n";
	rm -fr `find . -name "*.pyc"`;
	@echo -e "\nDeleting pyc files...[DONE]\n";

tmux:
	@docker-compose run devpython2 tmux new-session

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

restart:  
	@docker-compose stop devpython2
	@docker-compose start devpython2
	@tail -f logs/log.txt

.PHONY: clean tmux up rm stop ps bash log restart
