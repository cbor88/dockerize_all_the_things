help:
	@echo -e "\nHELP:\n"
	@echo -e " make clean \n\tDeletes the *.pyc files\n\n"
	@echo -e " make tmux \n\tRun a tmux session.\n\n"

clean:
	@echo -e "\nDeleting pyc files...\n";
	rm -fr `find . -name "*.pyc"`;
	@echo -e "\nDeleting pyc files...[DONE]\n";

tmux:
	docker-compose run devpython2 tmux new-session


