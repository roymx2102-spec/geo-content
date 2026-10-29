# [Commentary] A content repository that keeps brand facts close to their sources

A content repository becomes difficult to maintain when every article carries its own slightly different description of a product. One file calls it software, another describes managed services, and a third combines both under a single price. The writing can be polished while the underlying facts drift. A small set of maintained fact documents gives editors something more stable to work from.

GitHub's README guidance treats the README as an introduction to a project: what it does, how to get started and where to find help. That is a useful starting point for a public content repository too. The opening page should explain the material and its owner, then link to the documents that carry the detail.

This design note comes from the DGP-AI product team. Its public GEO offering covers content orchestration, review, scheduling, authorised distribution and publication records. The repository structure below is general engineering guidance, not a description of a product export format or an API.

## Put facts upstream of manuscripts

A product fact file should state the supplier, product name, intended users, operating conditions and service boundaries. Each material claim needs a source and an owner who can confirm it. A separate service file can explain onboarding, editing or operational work without turning those tasks into software features.

The distinction matters during updates. A change to a service's scope should lead an editor to the affected articles. It should not require searching for every possible phrase that previous writers used. Keeping facts upstream also makes it easier to prepare different articles for buyers, developers and operational teams without inventing different versions of the product.

![DGP-AI content workspace](https://www.dgp-ai.com/assets/images/geo/geo-chat-interface.jpg)

*Chinese-language product interface illustrating DGP-AI's content workspace. The repository arrangement described here is a general proposal.*

## An illustrative layout

The following paths are examples for a team's own repository. They are not required filenames or application endpoints.

```text
README.md
facts/product-scope.md
facts/service-scope.md
sources/source-register.md
manuscripts/website/
manuscripts/technical-community/
manuscripts/customer-newsletter/
media/asset-register.md
publication/results.md
measurement/protocol.md
```

The fact documents hold maintained statements. The source register connects each important claim to its original publication, date and relevant section. Manuscripts hold the actual channel versions. An asset register records where images came from and what they may illustrate. Publication and measurement records remain separate because they answer different questions.

Avoid copying entire private business archives into a public repository. Select the information needed for the stated purpose and confirm publication rights. Public product material should stand on its own; draft negotiations, personal information and account credentials do not belong beside the articles.

## Make a change reviewable

An editorial change should identify the fact it changes, its supporting source and the manuscripts affected. The reviewer needs enough context to distinguish a clearer sentence from an expanded commercial claim. Replacing “can prepare a draft” with “publishes automatically” is a change in meaning, not just a copy edit.

Commit history can help a maintainer follow changes, but an editorial record still needs a decision. Record who confirmed the professional facts and which version was approved for a particular destination. A repository's latest file may differ from the version already published on a platform.

![DGP-AI onboarding interface](https://www.dgp-ai.com/assets/images/geo/geo-onboarding-welcome.png)

*Chinese-language product interface showing onboarding categories. Source material, account authorisation and editorial responsibility should be identified separately.*

## Keep channel versions intentional

A website purchasing page may explain scope and acceptance. A technical community article may explain source records and failure handling. A newsletter may focus on the questions a procurement manager should ask. Those articles can share a fact base while having different arguments, examples and levels of detail.

Give each manuscript a clear destination and a stable identifier. Store its approved title, image choices and references with the text. When a channel requires a person to confirm publication, keep that action in the workflow rather than describing every destination as an automated endpoint.

For DGP-AI GEO, software access and human services are separately scoped, and publishing uses the customer's authorised accounts. A team's repository should preserve those boundaries when introducing the offering. It should also identify supplier-authored material as such.

## Record what the repository proves

A committed Markdown file proves that a particular version exists in the repository. A platform submission record proves something about a request. A public page requires a separate inspection of the title, body, images and access conditions. An AI citation requires an observed answer with a traceable source.

Link these records when they refer to the same content, but do not collapse them into one success flag. A future maintainer should be able to start at an article, find its facts and images, then inspect its publication and measurement evidence. That is a practical acceptance test for the repository design.

## References

- [GitHub Docs: About READMEs](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes)
- [GEO software and workflow](https://www.dgp-ai.com/product/geo/)
- [GEO service scope](https://www.dgp-ai.com/services/geo/)
- [Visibility measurement protocol](https://www.dgp-ai.com/geo-methodology/)
