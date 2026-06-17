**Static Token length:** Current Tokenization methods produce tokens of varying length
- is there value in producing fixed length tokens of size 2, 3, 4, or 5 with padded ends for elements that are too small.

**Tokenization method via distillation:**
- Initial tokenization by individual white spaces, individual non alphanumerics, alpha clusters, and numeric clusters
- secondary tokenization by length
  - pad all tokens where len < N with null tokens; split all tokens where len > N into (W/N) + 1 tokens where W is total word length
  - E.g. N = 2; word = jumps; output = [ ju,mp,s\x00 ]
  - research [BPE](https://en.wikipedia.org/wiki/Byte-pair_encoding) further and consider implementations for start, stop, unknown, etc.
  - These will act as semantic phonemes?
  - enough words are needed to generate every permutation, so 2 is probably ideal, 3 may be annoying
  - enough words are needed to link with all concepts, so the word dictionary may need to be re-evaluated

**Tokenization method via random gen:**
- generate all permutations of token size N
- create random vectors of size V and assign unige vectors to every token
  - the vectors won't have any meaning, but if the distillation method works, this should as well. meaning would have to be gathered via analyzing the model.