# Practical Walkthrough — NEURON-1 (Task 6)

> Consolidated hands-on challenge for Room 1. You operate a simulated neural network end-to-end to retrieve a flag.
>

## Objective

Drive a single input through the NEURON-1 network — input layer → hidden layer → output layer — and read the final classification to obtain the flag.

## Environment

- Browser-based simulated neural network (no external tooling required).
- Represents the architecture taught in Task 4: weighted connections between layers, with the hidden layer performing feature extraction.

## Approach

1. **Frame the network.** Confirm the three stages from Task 4 — input, hidden, output — and note that each connection carries a weight that scales the signal.
2. **Feed the input.** Provide the required input value(s) at the input layer, mirroring how a real model receives a feature vector.
3. **Traverse the hidden layer.** Follow the weighted signal through the hidden layer; this is where features are combined/extracted. Track how the activation changes rather than guessing.
4. **Read the output.** The output layer produces the network's decision. Interpret it as the model's prediction/classification.
5. **Retrieve the flag.** Correctly reading the output yields the challenge flag → `THM{<redacted>}`.

## Techniques / concepts applied

- Forward pass through a feed-forward network
- Weighted-sum → activation → output intuition
- Reading a model's output as a decision, not a black box

## Lessons

- The whole point of Room 1's practical is *interpretability*: you can only defend or attack a model if you can reason about how a signal flows to an output.
- This mirrors real model-interpretability work (later formalized with tools like SHAP/LIME in Room 2/6).

## Result

Flag captured. Foundation confirmed for the offensive/defensive material in Room 2 onward.
