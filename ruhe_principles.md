# design philosophy

## meta

  purpose of UI/UX
    > UI/UX is primarily about giving the player ACCURATE information about the current gamestate and the actions available to them

## approach
  DO
    >provide the best possible approximation of state to the user
      appropriate approximations include:
        deterministic predictions like
          - *you WILL act in 3 turns after the player before you*
          - *the tournament WILL start at 00:00 london time*
          - *your turn WILL end in 15 seconds after it starts*
        partial true information like:
          - *your raise action WAS sent to the server
            - and it IS being processed by the server's poker rules engine
            - and it WAS $666
            - and your stack WAS $2.0
              so the raise WILL fail*
                but the server will have to check that first
    > emphasize the most relevant parts of that state
      *if several players have made bets, one of those bets is going to be greater than others*
      *it's more important to know which player's turn it is than to know what their stack is, and then their stack is much more important than their username and avatar*
        *part of that is because players literally can't move between different seats or have someone else take their seat until a hand is finished*

  ¡DO NOT !
    > tell what the state MIGHT have been had some condition been different:
      *here's a grayed out create a private room button, if you had connected a wallet, then you could have created one*
      *here's a semi-transparent bet slider, if it were your turn, you could use it, but it is not...*
    > conceal relevant and true state for aesthetic purposes
      *
    > implicitly convey state and assume that the user remembers / infers / calculates it themselves, because they're high IQ elite human capital
      *its fine if the current raise isn't on the bet slider thumb and the minRaise isn't marked on the slider track anywhere, because you can just look at the raise button at the start of your turn and you can look at your stack and compare them, and you can also look at the raise button while you're dragging the slider thumb so it's fine.*

## emphasis
  ONLY
    > emphasize the important state
      *the player that's currently acting has a bright orange flame oval progress bar around their nameplate*
      *the player that folds gets a clear BLACK with a WHITE stripe oval line around their nameplate*

  NEVER
    > de-emphasize the less important state
      *the players that are not acting become slightly darker and semi-transparent, the player that is acting stays white as usual*
      *players that fold become slightly darker and semi-transparent, everyone else stays normal as usual*

## Discoverability
make sure everything the user could want can be discovered through an easy and obvious sequence of steps,
like settings -> visuals -> color theme, do not hide things behind unintuitive gestures, hovers, swipes,
mysterious more... or ">" buttons, do not assume the user is too stupid to understand self-explanatory titles
and needs to be protected from "advanced settings for turbocomplicated software nerds haha", lest they faint upon seeing them

## Controls
buttons should be recognizable by their position, shape and colour alone, they don't move around, 
you should be able to toggle things on and off by pressing in the exact same spot with muscle memory alone