[source of this document](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-entity-extractor)

## Define custom entities

Teach Discovery about terms that are significant to your business by creating an entity extractor.

An _entity extractor_ is a machine learning model that recognizes and tags terms that you indicate are significant to your business need or use case. When you create an entity extractor, you get to decide the content and scope of information to find and extract. Your extractor can extract any of the following things:

-   Terms that represent objects, such as vegetable names from cooking recipes or the make and model of cars from accident reports
-   Attributes of objects, such as color and quantity
-   Short phrases, such as `107 deaths in France`, `revenue of $343M`

An _entity type_ is a type of thing. To create an entity extractor, you define a set of _entity types_ that you care about. You then annotate a collection of your own documents by finding terms or phrases that represent the type of information you want to extract and labeling them as entity examples.

After you define entity types and label entity examples, you can generate a machine learning model. The model learns about the information that you care about based on how the terms or phrases that you label as examples are referenced in sentences. The model learns from the context and language with which the entity examples are referenced in the training data.

After the machine learning model is trained well enough to recognize your entity types, you can publish the model as an enrichment and apply the enrichment to new documents. The custom entity extractor enrichment recognizes and tags new mentions of the same and similar terms as occurrences of the entity types that you care about.

For more information about how to use the entity extractor to add domain customization to your AI applications, see the [Entity Extractor Feature in Watson Discovery v2](https://community.ibm.com/community/user/watsonai/blogs/ananya-poddar/2022/06/09/entity-extraction-in-watson-discovery-v2) blog post.

Discovery also has a built-in _Entities_ enrichment that can be applied directly to your collection. It doesn't require any training to recognize commonly-known proper nouns. For more information about the Watson NLP Entities enrichment, see [Entities](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-nlu).

You already built an entity type system in Knowledge Studio? You can use the corpus that is associated with your machine learning model as a starting point for your entity extractor training data. For more information, see [Importing a corpus](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-entity-extractor#entity-extractor-import-wks).

For information about the languages with which the entity extractor can be used, see [Language support](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-language-support).

## Example

If you are familiar with the built-in Entities enrichment, you know that the enrichment can recognize terms that match generalized categories, such as `Person` and `Location`. With the entity extractor, you control what constitutes terms or phrases that are meaningful.

The following image shows the terms that an enrichment that recognizes `family members` entity type mentions might extract from text. The example illustrates how family member mentions and other entity mentions (that are recognized by the built-in Entities enrichment) both might be predicted.

This excerpt comes from Chapter 3 of _Pride and Prejudice_ by Jane Austen.

## Before you begin

Find or create a collection with documents that have various examples of the entity types that you want Discovery to learn about. To teach the extractor, you must label examples of entity types. You can only label examples if your collection contains valid examples. Try to find documents that have many and varying terms that function as examples of every entity type that you want to define.

## Adding an entity extractor

To add an entity extractor, complete the following steps:

1.  Open the project where you want to create the entity extractor.
    
    The project must have at least one collection with documents that are representative of your domain data.
    
2.  From the _Improvement tools_ panel of the _Improve and customize_ page, expand **Teach domain concepts**, and then click **Extract entities**.
    
3.  Click **New**.
    
    If you want to create an entity extractor that is based on the entity type system from a IBM Watson® Knowledge Studio corpus, click the arrow, and then choose **Import a Knowledge Studio corpus**. For next steps, see [Importing a Knowledge Studio corpus](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-entity-extractor#entity-extractor-import-wks).
    
4.  Add an extractor name and optionally a description.
    
    This name is used as the model name and as the name of the enrichment that is created when you publish the model. The name is displayed as the enrichment name in the Enrichments page where you and others can apply it to collections. It also is displayed as the model name in the JSON representation of documents where custom entities are found. The name is stored with the capitalization and spacing that you specify.
    
5.  Choose a collection with documents that are representative of your domain data.
    
6.  Choose fields from the document to show in the document view where you will label documents from the collection.
    
    -   **Document title** is shown in the page header as the document name. Choose a field that has a unique value per document, such as the file name, which is stored in the `extracted_metadata.filename` field.
    -   **Document body** is where you label entity examples. Choose a field that contains the bulk of the document content, such as the `text` field.
    
7.  Click **Create**.
    

A document from the collection that you selected is displayed in the _Label documents_ view. You will label occurrences of the entity types that you want Discovery to recognize from this and other documents in the collection.

If no text is displayed in the body of the page, start over now by creating a new entity extractor. This time, when you select a value for the _Document body_ field, be sure to choose a field from your processed documents that contains text.

## Defining entity types

Define entity types by completing the following steps:

1.  Click **Add an entity type**.
    
2.  Add the entity type name and an optional description.
    
    Use a naming convention that works for your data. The built-in Entities enrichment uses initial capitals and no spaces, for example `EmailAddress`. To distinguish your entities from entities that are extracted by other enrichments, you might want to use a different convention.
    
3.  Optional: Pick the color to use for highlighting text in the document that you want to label as an example of this entity type.
    
    You can click a color from the _Label color_ palette, click the _Renew color_ icon to tab from one color to the next. To use a custom color, specify its hexadecimal color code (#fff0f7).
    
4.  Click **Create**.
    
5.  Repeat this process to add all of the entity types that you want the extractor to recognize.
    
    If you aren't sure what to add for entity types, it might help to review the documents in the collection first. By reviewing the content, you can get a feel for which terms have significant meaning and look for logical ways to group such terms.
    

## Label significant terms

From the _Label documents_ view, find terms of significance in the documents from your collection and label them to indicate their entity types.

Before you begin labeling documents, decide whether you want to keep bulk labeling enabled. The bulk label feature is a great way to speed up the process of labeling your documents. When enabled, every term that you label is labeled automatically everywhere it occurs in the document. Otherwise, you must label each occurrence of the term one at a time.

If you decide that you don't want to bulk label examples, set the **Bulk label entity examples** switch to **Off**. For more information, see [Labeling examples in bulk](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-entity-extractor#entity-extractor-bulk-label).

### Labeling tips

Review these tips before you begin:

-   The document collection that you label must contain a representative set of documents. The documents must have many and varied examples of the entity types that you want the entity extractor to recognize. If the collection you selected when you started to create the entity extractor does not meet the requirement, stop now and start over with a different document collection.
-   Define entity types that are clearly distinct from one another.
-   Aim to label at least 40 examples of each entity type.
-   Label every valid example of an entity type. Do not skip any occurrences. To speed up the process, use the bulk label feature.

### Labeling entity examples

Label terms in the document that represent examples of the entity types you defined. When you are done with one document, switch the document status from _In progress_ to _Complete_, and then move on to the next document.

To label entity examples, complete the following steps:

1.  Review the text of the document. Look for entity examples to label.
    
    The following table shows some examples.
    
    Entity types and examples
    - **color**: white, green, purple 
    - **car**: convertible, SUV, sedan
    - **auto\_model**: Explorer, Civic, Sorrento
    - **auto\_manufacturer**: Ford, Honda, Kia
    - **clothing**: shirt, blouse, skort
    - **instruments**: bonds, stocks, ETFs, munis
    
    If an entity type that you want to identify is not created yet, add the entity type. From the _Entity types_ panel, click **Create new**. For more information about adding entity types, see [Defining entity types](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-entity-extractor#entity-extractor-add-entities).
    
3.  First, click the entity type from the _Entity types_ panel.
    
4.  In the document body, select the word or phrase that represents the entity example.
    
    The term is selected and a color label is applied to the term. The first two characters of the entity type name are shown in uppercase superscript within the label boundary. Both the 2-character ID and the label color help you to associate the example with the entity type it represents.

    The example text is also added to the _Entity types_ panel. If you click the chevron to view details, you can see that the example is listed. The example text is saved in lowercase, regardless of the capitalization that is used in the original text.
    
5.  If bulk labeling is enabled, a notification is displayed to show the number of occurrences of the term that were found and labeled in the current document.
    
6.  If you want to label occurrences of the term in all of the documents in the collection, click **Apply to all documents**.
    
    When you enable this option, occurrences of the term are labeled in all of the documents in the collection, including documents that you already reviewed and marked complete.
    
    You are asked to confirm the action because it cannot be undone. If you don't want to have to confirm the action every time you choose to apply bulk labeling to all documents, select **Do not ask for confirmation again**. Click **Run**.
    
    For more information, see [Labeling examples in bulk](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-entity-extractor#entity-extractor-bulk-label).
    
7.  Scroll through the document to label every valid example of every entity type that you want your extractor to recognize.
    
    You can search for terms that you want to label as entity examples. For more information, see [Searching for examples by using keywords](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-entity-extractor#entity-extractor-search).
    
    The machine learning model learns as much from the terms that you don't label as the terms that you do.
    
    If you miss labeling a valid example, the model learns that when the term is used in that context, it is not a valid mention of the entity type. In some cases, an omission is appropriate. For example, some terms have different meanings in different contexts. You don't want to label the term when it is used in the wrong context. However, if the term is used in the right context and you don't label it, you are teaching the model to ignore it. You decrease the model's effectiveness when your training data is inconsistent.
    
    After you label many examples, entity example suggestions are displayed. You can accept or reject entity example suggestions.
    
    Accepting example suggestions is another way to speed up the labeling process. For more information, see [Entity example suggestions](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-entity-extractor#entity-extractor-suggestions). After you accept a suggestion, you can bulk label the term.
    
8.  If you make a mistake and label the wrong word or a word was labeled incorrectly by the bulk labeling process, you can delete the label.
    
    Hover over the labeled word until the **Delete this example** option is displayed, and then click it. You can choose to delete only this mention or all of the mentions in the document. Make a choice, and then click **Delete**.
    
9.  After you label all of the entity examples in the current document, change the document status from _In progress_ to **Complete**.
    
    Another document from the collection is displayed.
    
10.  Label examples of your entity types in each document in the collection.
    
    At any time during the labeling process, you can click **Save entity extractor** to save your work.
    
11.  If you don't have enough examples in the current set of documents, you can add more documents.
    
    From the _Document list_ panel, click **Add documents**. The option is available only when more documents are available in the collection. You can add up to 20 documents. If bulk labeling for all documents is enabled, labels are applied to the newly-added documents automatically.
    
11.  After you label examples in as many documents in the collection as you want, click **Save entity extractor**, and then open the _Train extractor_ page.
    

### Searching for examples by using keywords

Using the search feature, you can find entity examples in a document and label them easily. You can also use search to find labeled examples and unlabeled examples and correct any labeling inconsistencies.

To search by using keywords, complete the following steps:

1.  On the _Label documents_ view, click the _Find_ icon.
    
2.  In the **Find** field, specify a keyword to search in the document.
    
    The search results from the document are displayed when you enter the keyword.
    
    To browse the search results, you can click the _Next result_ and _Previous result_ icons. To choose a label for an unlabeled example in the result, click the _Edit label_ icon and select a label. You can also remove a label from an already labeled example in the result by clicking the _Edit label_ icon.
    
3.  To filter the search results, click the _Show filter options_ icon.
    
    The following table describes the filter options.
    
    Filter options in find
    - **All**: To find all examples in a document that match the keyword.
    - **Labeled text**: To find existing labeled examples in a document that match the keyword.
    - **Unlabeled text**: To find unlabeled examples in a document that match the keyword.
    - **Match case**: To find examples that match both the keyword and its case.
    - **Whole words**: To find examples that match the word boundaries of the keyword. For example, if you specify _york_ as the keyword, _yorktown_ is not matched when this option is selected.
    

For the unlabeled examples in the results, you can accept or reject a label suggestion.

To resolve any overlapping examples, click **Review suggestions** and choose an entity example suggestion from the _Overlapping entity example suggestions_ dialog box.

### Labeling examples in bulk

For most entity examples, enabling the bulk label feature is helpful. You might want to skip it if a term has more than one meaning in different contexts. In that case, evaluate each occurrence individually. Remember, if you enable the bulk label feature, you can check the accuracy of the labels that were added automatically and make corrections when necessary as you review the document.

After you enable the bulk label feature, a notification is displayed that indicates how many occurrences of an entity example were found in the current document. From the current page, the labeling tool cannot access other documents to report how many occurrences exist in other documents from the collection. However, the mention count is shown in the _Entity types_ panel. When you first open other documents, you can check the mention counts to see how many mentions were labeled automatically.

Did the bulk label feature miss an occurrence?

Occurrences of the term are not labeled if they occur in the same phrase in which the term is already labeled. For example, the first occurrence of the term `husband` is not labeled when the bulk label feature is switched on for the second occurrence of the term in the following sentence.

### Entity example suggestions

After you label enough examples, suggested entity type examples are displayed. The system learns from the types of examples you label, and applies what it learns to identify potential new examples. For example, after you label `red`, `orange`, `yellow`, `green`, and `blue` as examples of the `color` entity type, the _Example suggestions_ panel might show `indigo` and `violet` as suggested examples for you to label. Suggestions are not displayed until after you label many examples of an entity type.

The following example shows suggestions that are made for family member mentions.

You might notice that a term that you chose to bulk label is not labeled, but is displayed as a suggestion instead. A term is skipped in the following situations:

-   The term might occur in different noun phrases in different sections of the document. For example, the term `father` might occur in the noun phrases `the kindest *father*` and `to her *father*`. When a word is included in a noun phrase with adjectives, the meaning can change. Therefore, such terms sometimes are suggested rather than labeled automatically.
-   A word might be a valid example on its own and as part of a multiple-word mention. For example, a mention of `IBM` might refer to the company _International Business Machines, Corp._ or might be used as part of a product name, such as _IBM Cloud Pak for Data_. However, a word or phrase can be part of only one example. Example labels cannot overlap one another. Therefore, you must choose which example suggestion is the most accurate. In this example, where the term _IBM_ is used as part of a product name, it is more accurate to label the full phrase as an example of the `Product` entity type.
-   The service might recognize that a term is a possible example of more than one entity type. For example, the word `top` might mean _the best_ or might mean _shirt_.

To investigate a suggestion further, click it to see the word in context within the document. Seeing the term in context helps you to decide whether the occurrence is a valid entity example for you to label.

### Exporting labeled data for an entity extractor

You can export the labeled data for an entity extractor from Discovery. You can use the exported labeled data for training or building large language models (LLMs) on a service such as Watson Studio and Natural Language Processing (NLP).

To export the labeled data, complete the following steps:

1.  From the _Improvement tools_ panel of the _Improve and customize_ page, expand _Teach domain concepts_, and then click _Extract entities_.
    
2.  For the entity extractor from which you want to export labeled data, click the _Actions_ icon, and then select **Download labeled data**.
    
    A compressed file is downloaded with labeled data. The compressed file contains the following JSON files.
    
    -   `labeled_data.json`: Includes the text and labels. The data format is based on the input data format for entity extraction in Watson Natural Language Processing. For more information, see [Input data format](https://www.ibm.com/docs/en/watsonx-as-a-service?topic=models-detecting-entities-custom-transformer-model#input-data-format).
    -   `metadata.json`: Includes metadata for the workspace and labeled data.

## Importing a Knowledge Studio corpus

For installed deployments, the import capability was added with the 4.6.2 release.

You can import a corpus of documents that were annotated in IBM Watson® Knowledge Studio to use as the training data for an entity extractor in Discovery.

Entity types that were defined in Knowledge Studio are shown as new entity types in Discovery. You can continue to annotate the imported documents when you customize the entity extractor model.

Entity subtypes and relations from the Knowledge Studio machine learning model are not represented, neither are any custom dictionaries that are associated with the model.

Before you can import a corpus, you must export the document set from Knowledge Studio as a .zip file. Follow the appropriate steps for exporting based on your Knowledge Studio deployment type:

-   [IBM Cloud](https://cloud.ibm.com/docs/watson-knowledge-studio?topic=watson-knowledge-studio-exportimport#wks_exportimport_expimp_doc)
-   [Cloud Pak for Data](https://cloud.ibm.com/docs/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-exportimport#wks_exportimport_expimp_doc)

Although you must download both the document set and type system to include annotations in documents that you upload to another Knowledge Studio workspace, the same is not true in this use case. You import only the document set to Discovery. Any annotations in the documents are recreated in Discovery. The Knowledge Studio type system is not needed.

To import a Knowledge Studio corpus, complete the following steps:

1.  Open the project where you want to import the corpus.
    
2.  From the _Improvement tools_ panel of the _Improve and customize_ page, expand **Teach domain concepts**, and then click **Extract entities**.
    
3.  Click the arrow that is associated with the _New_ button. and then click **Import a Knowledge Studio corpus**.
    
4.  Add an extractor name and optionally a description.
    
    This name is used as the model name and as the name of the enrichment that is created when you publish the model. The name is displayed as the enrichment name in the Enrichments page where you and others can apply it to collections. It also is displayed as the model name in the JSON representation of documents where custom entities are found. The name is stored with the capitalization and spacing that you specify.
    
5.  Click **Upload**, and then browse to find and select the .zip file that you exported from Knowledge Studio. Click **Create**.
    
    The annotated documents that you upload are stored with the entity extractor workspace, not as a new collection in the project. You can continue to annotate the documents.
    

Give Discovery some time to import and process the machine learning model corpus. After the entity extractor is created, the extractor is opened to the _Label documents_ page.

## Training the extractor

After you label documents, review the training data that will be used to train the entity extractor model.

To train the extractor, complete the following step:

1.  Decide whether you want to apply an advanced option. Most models do not require changes to these options.
    
    The following customizations are available from the _Review and finish_ page:
    
    -   Include documents that were not reviewed by a person in the training set.
        
        Typically, only documents that a person labeled, reviewed, and explicitly marked complete can be candidates for inclusion in the training set. However, if you want to allow documents that were not marked complete to be included in the training set, you can do so.
        
    -   Change the ratio of documents that are included in the document sets that comprise your training data.
        
        The documents from your collection are split at random into the following sets:
        
        -   Training set: The documents that you label and that are used to train the entity extractor machine learning model. The goal of the training set is to teach the machine learning model about correct labels.
        -   Test set: The documents that are used to test the trained model. After you run a test, you can review the results, closely analyze areas where the model got something wrong, and find ways to improve the model's performance.
        -   Blind set: Documents that are set aside and used to test the model periodically after several iterations of testing and improvement are completed. The documents in the blind set are intentionally roped off. As you test the model with documents from the test set and analyze the results, you become familiar with the underlying test documents. Because the test documents are used iteratively to improve the model, they can start to influence the model training indirectly. That's why the blind set of documents is so important. The blind set gives you a way to generate an unbiased evaluation of the model periodically.
        
        The default split applies a ratio (70%-23%-7%) that is commonly used for machine learning training.
        
2.  Click **Train extractor**.
    

When you train the extractor, Discovery uses documents from the training set to build a machine learning model. After the model is generated, it runs a test against the documents from the test set automatically. The results of the test are displayed for you to review.

### Troubleshoot training issues

Learn about possible error messages and how to address them.

The training data is too large

Your training data contains large text document or many entity types and resources that are needed to process the data is greater than the resources that are available to your service instance. This error can occur even when your workspace doesn't exceed the documented entity extractor limits. To resolve the issue, you can try one of the following approaches:

-   Remove one or more entity types to decrease the size of your training data.
-   Remove extra large documents from the training data. For example, if one of the labeled documents is extra large, change its status from _Completed_ to _In progress_ to omit it from the training data.
-   Reduce the number of documents that are included in the training set. The default split ratio (70%-23%-7%) for the training data uses 70% of the documents in the training set. You can change the percentage of documents that are used in the training set to a smaller number. For example, you might change the split ratio to 60%-33%-7%.
-   Increase the capacity of your deployed service instance by scaling up service pods.

## Evaluating the extractor

To review metrics from the test run of the entity extractor model that you created, click the **Evalute extractor** tab.

The following table describes the available evaluation metrics.

Metrics details
- **Confusion matrix**: A table that provides a detailed numeric breakdown of annotated document sets. Use it to compare entity type mentions that are labeled by the machine learning model to entity type mentions that are labeled in the training data.
- **F1 Score**: Measures whether the optimal balance between precision and recall is reached. The F1 score can be interpreted as a weighted average of the precision and recall values. An F1 score reaches its best value at 1 and worst value at 0. Overall scores are lower if the model doesn't have enough training data to learn from.
- **Precision**: Measures how many of the overall extracted mentions are classified as the correct entity type. A false positive is when an entity should not be extracted, but was extracted(Predicted = Positive, Actual = Negative). False positives typically mean low precision.
- **Recall**: Measures how often entity type mentions that should be extracted are extracted. A false negative is when an entity type should be extracted, but was not extracted (Predicted = Negative, Actual = Positive). False negatives typically mean low recall.

1.  Review the metrics that are provided about the extractor model test run to determine whether more training is needed.
    
2.  Explore the test results in more detail by clicking **Review training results in test set**.
    
    Documents from the test set are displayed with the predicted labels shown in one panel and the ground truth shown in the other.
    
    -   Predicted labels are the examples that the entity extractor identified and labeled as entity types.
    -   The _ground truth_ has examples that a person labeled or that were bulk labeled and reviewed by a person. Labels in the ground truth are considered the correct labels.
    
    The performance of the model is rated based on how closely the predicted labels match the ground truth.
    

### Improving the extractor

The following table shows suggested fixes for common problems.

Improvement actions
- **Low overall scores**: You might not have enough documents with labeled examples in your training set. Label more examples in more of your documents.
- **Low recall**: Label more documents with new examples of the entity types that the extractor missed.
- **Low precision**: Look for entity types that are commonly confused. Find and label more examples of each entity type to help the entity extractor distinguish between the entity types.

### Adding documents to the training data

To add more documents, complete the following steps:

1.  Open the _Label documents_ tab.
    
2.  From the _Document list_ panel, choose **Add documents**.
    
    This button is disabled if no other documents are available to add to the entity extractor from the current collection. To add more documents to the collection, go to the _Activity_ page for the collection, and then click the _Upload data_ tile to browse for and add more files.
    

You cannot choose the documents from the collection to show in the _Document list_ for labeling purposes. If there are specific types of documents that you want to label, consider adding representative documents to a collection that you can use to create the entity extractor.

There are limits to the number of documents that can be included in the training data. If your training data includes documents with a combination of sections that are labeled and others that are not, the system might sample some examples from unlabeled sentences. Subsampling helps to balance the number of positive and negative examples that are used for training. Balancing the examples in the training set improves the training performance.

## Publishing the entity extractor as an enrichment

When you think the entity extractor is ready, publish the entity extractor. How do you know when it's ready? If the score doesn't change after several test runs in which you make improvements, the model is ready. You can return to update and retrain the model after you publish it.

1.  From the _Evaluate extractor_ page, click **Publish extractor**.
2.  Click **Apply to data**.
3.  Choose a collection, and then select the document field where you want the entity extractor enrichment to be applied.
4.  Click **Apply**.

## Exporting the entity extractor

For installed deployments, the export capability was added with the 4.6.2 release.

An entity extractor model that you create and deploy in one project is available as an enrichment that can be applied to a collection from any project in the same service instance.

If you want to use the entity extractor model in a project from another service instance, you can export the entity extractor. To use it elsewhere, follow the steps to create a machine learning model from [Use imported ML models to find custom terms](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-domain-ml). You cannot continue to edit an entity extractor that you import into another project.

The entity extractor that you want to export must be fully trained.

To export an entity extractor, complete the following steps:

1.  Open the project with the entity extractor that you want to export.
    
2.  From the _Improvement tools_ panel of the _Improve and customize_ page, expand _Teach domain concepts_, and then click **Extract entities**.
    
3.  From the _Entity extractors_ list, find the entity extractor that you want to export.
    
4.  Click the _Actions_ icon for your extractor, and then choose **Download model** to save the model to your system.
    
    The _Download model_ option is not available unless the model is trained.
    

The entity extractor model is saved as a .ent file. You can import it into a project in another service instance as a machine learning model, and then apply it to your collections. For more information about importing the model, see [Use imported ML models to find custom terms](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-domain-ml).

## Applying an entity extractor enrichment

When you publish the extractor, you specify the field where you want the extractor to be applied. If you decide to apply the enrichment to different or more fields later, you can follow these steps to do so.

1.  From the navigation panel, click **Manage collections**.
2.  Click to open the collection where you want to apply the enrichment.
3.  Click **Enrichments**.
4.  Find the entity extractor name in the list, and then choose a field to apply the enrichment to.
5.  Click **Apply changes and reprocess**.

For more information about how to remove an entity extractor enrichment from a collection, see [Managing enrichments](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-manage-enrichments).

### Entity extractor output

When the enrichment recognizes one of your custom entities in a document, an entry is added to the `enriched_text.entities` section of the JSON representation of the document. The section contains occurrences of entities that are recognized by your custom model along with entities that are recognized by the built-in Entities enrichment. The built-in enrichment uses the Watson NLP service to identity entites that are part of what it calls the _Natural Language Understanding_ type system. For more information about the built-in Entities enrichment, see [Entities](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-nlu#nlu-entities).

The following JSON output is produced by a custom model that is named _literature_ that recognizes family member mentions.

### Monitoring performance over time

You can retrain your entity extractor model at any time. Each time that you train the model, review the performance metric scores to determine whether your most recent changes increase or decrease the model's scores.

1.  To compare one test run against another, click **View score history**.
    
    The history view shows the last 5 training runs.
    
    To retain the score information for more than the most recent 5 training runs, you can export the metrics in comma-separated value format, and track the scores in a separate application. Click the tabular representation icon ![Tabular representation icon](https://cloud.ibm.com/docs-content/v4/content/966e10d2c52b59673478a25d7ef6d3e13b740494/discovery-data/images/table-of-contents.svg), and then click **Download as CSV**.
    

If a subsequent training run results in lower scores, don't publish that version of the model.

## Deleting an entity extractor

You can delete an entity extractor if it is not in use, meaning the enrichment that is published from the entity extractor is not applied to a collection.

You might want to delete an entity extractor if you hit the limit for the maximum number of extractors that are allowed for your plan, for example.

Remember, limits are defined per service instance, not per project. If you cannot create new entity extractors, but do not have the maximum number of extractors in the current project, check other projects in the same service instance. There might be entity extractors that aren't being used in other projects that can be deleted.

1.  Remove the entity extractor enrichment that was published from the entity extractor that you want to delete from any collections where it is being used.
    
    For more information, see [Deleting enrichments](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-manage-enrichments#enrichments-delete).
    
2.  From the _Improvement tools_ panel of the _Improve and customize_ page, expand **Teach domain concepts**, and then click **Extract entities**.
    
3.  Find the entity extractor that you want to delete, click the _Actions_ icon, and then select **Delete**.
    

## Entity extractor limits

The number of entity extractors that you can create per service instance depends on your Discovery plan type.

Entity extractor plan limits (Entity extractors per service instance /	Maximum entity types per extractor / Maximum documents in training data)
- **Cloud Pak for Data**: Unlimited / 18 / 1,000
- **Premium**: 10 / 18 / 1,000
- **Enterprise**: 10 / 18 / 1,000
- **Plus (including Trial)**: 3 / 12 / 200
