Test your Othello program
--------------------------
This folder contains code for testing your Othello program. 

On a linux machine, do the following:
- Make sure that the scripts 'othellostart' and 'othello' are executable. If not, write `chmod +x othellostart othello_naive`.

- Run the 'othellostart' script with three parameters, indicating which programs should play against each other and a time limit:
  - `./othellostart` *`white_player`* *`black_player`* *`time_limit`*
  
  - For instance, if you have placed your `othello.sh` script in `~/othello/`, you can benchmark against the naive baseline with a 5s time limit by running `./othellostart ./othello_naive ~/othello/othello.sh 5`

  - If you would like to play against a friend, just replace ./othello_navive with the correct path to your friend's script
