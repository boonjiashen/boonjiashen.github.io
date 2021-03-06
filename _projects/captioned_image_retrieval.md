---
title: "Robust image retrieval using topic modeling on captioned image data"
pdf: Robust_image_retrieval_using_topic_modeling_on_captioned_image_data.pdf
date: "Jun 8, 2015"
type: "CS766 Computer Vision course project"
github: https://github.com/msyamkumar/captioned_image_retrieval_CS766_final
authors:
  - Jia-Shen Boon
  - Akshay Sood
  - Meenakshi Syamkumar
---
Image retrieval based only on image features emphasizes only visual similarity and does not capture semantic similarity between images. In order to capture the semantic similarity textual data associated with images can be very useful. We demonstrate that some semantics of an image, while poorly captured by the image alone, can be captured by text that accompanies the image. These semantics include artistic feel and sociocultural events. We capture these semantics by modeling the topics generated by the accompanying text, referred to as captions, whie visual features are extracted with a deep convolutional network. A joint model of text and images is applied to the Flickr8K dataset. We also collect a custom dataset of over 32K images and 110K captions, crawled from Imgur. This model has applications in general to image retrieval, as well as generating links to similar images within popular photo-sharing websites such as Imgur. In the latter application, such links would allow users to ‘account-hop’, which would increase visitor stay duration.
