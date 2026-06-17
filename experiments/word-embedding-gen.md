Method 1:
- Given a predefined mapping (V) between words and concept vectors 
- break all words into tokens (T) of size W/N + 1 where W is word length and N is token Length
  - pad all tokens that have lengths less than N
  - generate all sub tokens; so given N = 3; C = total characters, total tokens <= C^3 + C^2 + C^1 total tokens.
- duplicate a given word's V to all of it's child tokens
- calculate average(V) group by T
- Test token concatenation  with itself multiple times as well as passing the token to another layer (both reduced and expanded).
  - do either of these act like composition of concepts?
- Test token concatenation with undefined vector space.
