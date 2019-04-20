Note: this lab was based on the arg-opt choices file that was uploaded on Tuesday. This file had a particularly messy lexicon and affixes that led to many items not parsing correctly, if at all. More on this below. Kristen uploaded a new choices file on Friday afternoon that alleviates this issue, but that was a little late for us to migrate all our existing work. Therefore we proceeded with the old choices file, and plan to adapt the new one for the next week.

1. Changed made to the choices file:

   1. Added language name
   2. Specified word order, determiner status and order, and auxiliary verb information
   3. Added finite/non-finite FORM feature distinction because the customization webpage complained
   4. Specified that a determiner is optional for all noun lexical categories, because the descriptive material does not  definitively say if it's required or forbidden.

2. Initial run results:

   1. Test corpus
      1. 1 item parsed (3750@@@@1@@Daguma-j-ba wurlu-ngg-u@@@@1@2@hit-TH-FUT 3.DU.A-RR-FUT // They two will fight .@@)
      2. 1 parse for that item
      3. 1 parse for that item
      4. No source of ambiguity
      5. Unfortunately the semantics is wrong for that item. This seems to be a result of AGGREGATION considering "Daguma-" as a inflectional prefix instead of a lexical category.
   2. Test suite
      1. None parsed
      2. None parsed
      3. None parsed
      4. None parsed
      5. None parsed

3. Phenomena added

   1. Case

      - We took sentences that are marked with proper case from our descriptive material and substituted the words with simple ones as we can to form grammatical examples. We then modified the case to inappropriate ones to form bad examples. We show two examples here, and more below in Section 4 (choices made).

        ```
        Source: a:page
        Vetted: f
        Judgment: g
        Phenomena: {case}
        Alaji gi-n alalangmi.
        boy.I.NOM 3.SG.S(PR)-PROG hunt
        `The little boy is hunting.'

        Source: a:page
        Vetted: f
        Judgment: u
        Phenomena: {case}
        Alaji-ji gi-n alalangmi.
        boy.I-LOC 3.SG.S(PR)-PROG hunt
        `The little boy is hunting.'
        ```

        ​

4. Choices made

   1. First of all, as a preliminary to all our three phenomena, we added the four genders of Wambaya, which was absent in the original choices file.

   2. Case — Wambaya nominals take the form of "Root + (deriv) + (adnom) + (number) + gender# + ([GEN + gender*]) + (case)". In this section we model the genitive slot and the case slot. In order to do this, we made the following changes:

      1. The initial choices file only have nom, acc, erg, loc, gen, and dat. This is far from complete to cover all Wambaya cases. According to our descriptive material, we added allative, ablative, commutative, permeative, and causal cases. E.g.

         ```
         Source: a:page
         Vetted: f
         Judgment: g
         Phenomena: {case}
         Yarru g-amany gagarra-ngani.
         go 3.SG.S-PST.TWD east-ABL        
         `He came from the east.'
         ```

      2. We identified the position class that cases go in the existing choices file. Then, except for genitive case, if a case above was not in that position class, we add it in.

      3. Likely due to the nominative suffix is zero, the initial choices file mistakenly consider some lexical items as having inherent nominative case. We removed those inherent cases, because we already have a lexical rule that adds zero nominative suffix.

      4. We used a separate position class to cover the genitive case. And it has to precede the case position class, which we use position class dependency to model. E.g.

         ```
         Source: a:page
         Vetted: f
         Judgment: g
         Phenomena: {case}
         Mirra ngi alangi-niganka-ni jalyu-ni.
         sit 1.SG.S(PR) boy.I-GEN.IV-LOC bed.IV-LOC
         I’m sitting on the boy’s bed.

         Source: a:page
         Vetted: f
         Judgment: u
         Phenomena: {case}
         Mirra ngi alangi-ni-niganka jalyu-ni.
         sit 1.SG.S(PR) boy.I-LOC-GEN.IV bed.IV-LOC
         I’m sitting on the boy’s bed.
         ```

      5. Wambaya genitive case has agreement with three of the four genders: gender I, II, and IV. We added a lexical rule type for each, as well as the corresponding lexical rule instances. In particular, genitive case for gender IV has three allomorphs, so it has three instances. This agreement is also demonstrated in the grammatical example above.

5. Final run results:

   1. Unfortunately, because the many issues with the lexicon of the choices file, we still get only 1 item parsed for the test corpus and none for the test suite after improving the three phenomena above. We tried controlling the vocabulary for the test suite, but there are some other weird issues (LKB not combining constituents while interactive unification allows it). We anticipate this will get better next week when using the updated choices file from Kristen.

6. As mentioned above, the starter grammar did not have gender, and we had to add that. And of course our test suite illustrates the three phenomena above which the starter grammar didn't handle properly.

7. There were many issues with the lexicon, for example lexical categories considered as functional affixes and vice versa. But this seems to be resolved with the Friday afternoon version of the choices file. Another issue is the strange categorization of both lexical categories and affixes, where those that should belong in the same class are separated and vice versa. For example, from what we have read, Wambaya nouns seems to only belong to four gender categories, but the starter grammar gives around 10-20 of them.