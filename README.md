import random
import string
def build_markov_chain(text, n=1):
    markov_chain = {}
    for i in range(len(text) - n):
        state = text[i:i+n]
        next_char = text[i+n]
        if state not in markov_chain:
            markov_chain[state] = {}
        if next_char not in markov_chain[state]:
            markov_chain[state][next_char] = 0
        markov_chain[state][next_char] += 1
 # Convert counts to probabilities
or state, transitions in markov_chain.items():
        total = sum(transitions.values())
        for char in transitions:
            transitions[char] /= total
return markov_chain
def generate_text(markov_chain, length=100, seed=None):
    if seed is None:
        seed = random.choice(list(markov_chain.keys()))
    current_state = seed
    output = [current_state]
 for _ in range(length - len(seed)):
        if current_state not in markov_chain:
            break
        next_char = random.choices(list(markov_chain[current_state].keys()), 
                                   list(markov_chain[current_state].values()))[0]
        output.append(next_char)
        current_state = ''.join(output[-len(seed):])
 return ''.join(output)
# Example usage
text_corpus = "This is an example text corpus. It is used for building a Markov chain."
markov_chain = build_markov_chain(text_corpus, n=1)
generated_text = generate_text(markov_chain, length=200)
print(generated_text)
