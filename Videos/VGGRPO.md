##### Link: https://arxiv.org/abs/2603.26599
##### Authors: [Zhaochong An](https://arxiv.org/search/cs?searchtype=author&query=An,+Z), [Orest Kupyn](https://arxiv.org/search/cs?searchtype=author&query=Kupyn,+O), [Théo Uscidda](https://arxiv.org/search/cs?searchtype=author&query=Uscidda,+T), [Andrea Colaco](https://arxiv.org/search/cs?searchtype=author&query=Colaco,+A), [Karan Ahuja](https://arxiv.org/search/cs?searchtype=author&query=Ahuja,+K), [Serge Belongie](https://arxiv.org/search/cs?searchtype=author&query=Belongie,+S), [Mar Gonzalez-Franco](https://arxiv.org/search/cs?searchtype=author&query=Gonzalez-Franco,+M), [Marta Tintore Gazulla](https://arxiv.org/search/cs?searchtype=author&query=Gazulla,+M+T)
## Problems
- Video diffusion fails at preserving geometry.
- Other approaches improve geometry by
	- Augmenting the generator with additional modules
	- Applying geometry-aware alignment
	- *They compromise the generalizability of the model*
	- *The rewards are also in pixel space requiring VAE decoding, making the compute high*
	- *The works doing DPO or other RL based post-training also use off-line preference rewards*
## Potential Applications
- Embodied AI
- Physics simulations

#### Their proposed model is a latent geometry-guided framework for geometry-aware video post-training

They also have a latent geometry foundation model called *LGM* which stitches video diffusion latents to *geometry foundation models*.
They use **GRPO** in the latent-space with two complementary rewards:
- A camera motion smoothness reward that penalizes jittery trajectories
- A geometry re-projection consistency reward that enforces cross-view geometric coherence

![[vggrpo.pdf]]


### Brief Method Explanation
- Take input frames, put them through a geometry foundation model which works in pixel space
- Take the diffusion model's VAE, put that through its own *latent-space* layer and align the losses like distillation
- Next part is use LoRA layers for doing post-training fine-tune. The de-noised latent model spits out will have two rewards:
	- 