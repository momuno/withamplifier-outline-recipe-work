# What's in This Repo

Three documents that work together:

1. Outline (withamplifier-content.json) - Maps to the existing content section of withamplifier.com
2. Recipe (website-content-generation.yaml) - Creates website content from the outline 
3. Example Output (website-content.json) - Structured content ready to integrate into the existing website

## Outline Features

The outline includes some useful metadata:

- Accuracy levels - Indicates whether content should be marketing-creative, synthesized, or verbatim
- Community links - Provides real, working links for the community carousel
- Alternative headings - Suggests variations for some section titles (this emerged organically)

# How to Use This

## Getting Started

1. Load the sessions for reference as needed (not included in this repo...)
2. Review the example output and see if it can be ingested into your website

## Iterate on the Recipe

1. Ask Amplifier to run the recipe on the outline
2. Use recipe-author and recipe-validator to review results
3. Work with Amplifier to improve the outline where needed
4. Keep iterating until it works for you

## Extend to Other Pages

Once you have a working outline + recipe combination, use it as a template. For example, the support page has different needs—talk to Amplifier and iterate on both the outline and recipe to fit that page.

## Future Recipes to Consider

- Validation recipe - Is website content still accurate according to its claimed sources?
- Change detection recipe - If referenced source content changes, flag potential inaccuracies
- New module detection recipe - Surface new features, repos, deprecations, etc. and flag when the website needs updating (likely driven by amplifier/docs/modules.md)
