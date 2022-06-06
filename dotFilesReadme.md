## How to Push an Existing Project to GitHub [SOURCE](https://www.digitalocean.com/community/tutorials/how-to-push-an-existing-project-to-github#add-new-remote-origin-in-this-case-github)
- Step 1: Create a new GitHub Repo
	- Skip initialize repository
## The best way to store your dotfiles: A bare Git repository [SOURCE](https://www.atlassian.com/git/tutorials/dotfiles)

`git init --bare $HOME/.cfg
alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'
config config --local status.showUntrackedFiles no
echo "alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'" >> $HOME/.bashrc`

- The first line creates a folder ~/.cfg which is a Git bare repository that will track our files.
- Then we create an alias config which we will use instead of the regular git when we want to interact with our configuration repository.
- We set a flag - local to the repository - to hide files we are not explicitly tracking yet. This is so that when you type config status and other commands later, files you are not interested in tracking will not show up as untracked.
- Also you can add the alias definition by hand to your .bashrc or use the the fourth line provided for convenience.
- Set the flag showUntrackedFiles to no on this specific (local) repository:

	config config --local status.showUntrackedFiles no

- Prior to the installation make sure you have committed the alias to your .bashrc or .zsh:

	alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'

- And that your source repository ignores the folder where you'll clone it, so that you don't create weird recursion problems:

	echo ".cfg" >> .gitignore

## Helpful commands to know
- Checkout the actual content from the bare repository to your $HOME

	config checkout
	config status
	config add .vimrc
	config commit -m "Add vimrc"
	config add .bashrc
	config commit -m "Add bashrc"
	config push
