# card-games
 A collection of Python classes and scripts for using card games in Monte Carlo simulations and Machine Learning.

# Deck.py
Deck.py is a class for a deck of cards. An instance of this class holds an array of 52 strings representing cards. Card strings consist of the face value and a suit seperated by a hyphen. Face values { A, 2, ... Q, K } are represented as { 1, 2, ... 12, 13 }. Suits are { 's', 'd', 'c', 'h' }. Some examples of valid card strings are '1-s' for the ace of spades, '4-c' for the four of clubs, and '12-h' for the queen of hearts.

Usage:

from Deck import Deck
deck = Deck()

Functions
	
deck.shuffle()
returns the array to 52 randomly organized card strings.

deck.deal()
removes a card string from the Deck object, and returns it

deck.checkDeck()
prints the current content of the deck


# blackjack.py
Blackjack.py is an implementation of the classic card game using the Deck class, and played from the terminal. This script is used to generate data about hands of blackjack via Monte Carlo simulations. This is done by generating random hands and storing representations of the hands, tagged with the eventual outcome of the decision.

# representing a hand of blackjack

For the purpose of training a nuerel network to play blackjack, we want to represent a hand in a way that tells us whether we should 'hit' or 'stay.' Luckily we only need to know the value of the hand, so we represent each scenario as a single integer, ie. a hand of ( 2-s, 10-h ) will be 12. We then tag the data as either 'h' or 's' for 'hit' or 'stay.'

How we determine whether the hand warrants a 'h' or 's' is a matter of opinion. The current iteration will simply append in the following manner:

<pre>
if user hits and busts:
	tag = 's'
elif user hits and doesn't bust:
	tag = 'h'
elif user stays and wins hand:
	tag = 's'
elif user stays and loses hand:
	tag = 'h'
</pre>

Example scenarios and expected data:

<pre>
Example 1

player hand: ( 3-s, 4-c )
player hits
player hand: ( 3-s, 4-c, 12-d )
player stays
dealer busts

generated data and tags:
(because we won the game, we assume every move was a good move)
7,  h # hit on 7
19, s # stay on 19

Example 2

player hand: ( 2-d, 10-c )
player hits
player hand: ( 2-d, 10-c, 2-s )
player hits
player hand: ( 2-d, 10-c, 2-s, 9-c )
player busts

generated data and tag

12, h
14, s
</pre>



