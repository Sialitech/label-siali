---
title: Project components 
short: Project components 
# type: guide  # this page is not ready, so remove it from everywhere
# tier: all
order: 118
meta_title: Project components 
meta_description: "Siali Label Documentation for Project components."
section: "Configuration"
---


This page describes the general project components in the Siali Label UI. 


## Labeling interface 

The Siali Label interface allows you to label and annotate your data. You can start labeling and annotating your data only after you setup your project, labeling interface, and import your data. For more information, see the [Label and annotate data](labeling.html#Start-labeling) page. 


## Annotation

Annotation is the process of labeling data on images. The image may contain humans, vehicles, any objects to make it recognizable for machines. Annotations are of various types, and it can be used to educate machines about the presence of various objects in the world. For more information, see the [Label and annotate data](labeling.html#Start-labeling) page. 

<div class="enterprise-only">

## Review 

After multiple labelers have annotated tasks, review their output to validate the quality of the results. For more information, see the [Review annotations in Siali Label](quality.html) page.

## Members 

In the Siali Label Enterprise version, you can add members to a specific workspace or add members to a specific project within a workspace. For more information, see [Add members to a project](setup_project.html#Add-members-to-a-project) page. 

</div>

## Machine Learning 

Use the Siali Label ML backend to integrate Siali Label with machine learning models.  For more information, see [Integrate Siali Label into your machine learning pipeline](ml.html) page. 


## Cloud Storage 

You can add source storage connections to sync data from an external source to a Siali Label project, and add target storage connections to sync annotations from Siali Label to external storage. For more information, see [Sync data from external storage](storage.html) page. 


## Webhook 

Webhooks in Siali Label allows you to set up integrations that subscribe to certain events which occur inside Siali Label. When an event is triggered, Siali Label sends an HTTP POST request to the configured webhook URL. For more information, see [Set up webhooks in Siali Label](webhooks.html) page. 
