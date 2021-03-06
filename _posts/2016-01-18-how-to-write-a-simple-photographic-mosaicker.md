---
layout: post
title: How to write a simple photographic mosaicker
type: post
published: true
status: publish
categories:
- computer vision
tags: []
meta:
  _publicize_pending: '1'
  _edit_last: '81887416'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1463375082;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:180;}i:1;a:1:{s:2:"id";i:16;}i:2;a:1:{s:2:"id";i:28;}}}}
  original_post_id: '146'
  _wp_old_slug: '146'
---

<p>Today we'll learn how to write a simple photographic mosaicker! You've probably seen those large pixelated images that are composed of tiny irrelevant images, like a portrait of Obama that comprises tiny cat pictures. These are known as <strong>photographic mosaics. </strong>Here I'll describe a very simple approach to creating such a mosaic, using <a href="https://en.wikipedia.org/wiki/Nearest_neighbor_search">nearest neighbor search</a> and the<a href="https://www.cs.toronto.edu/~kriz/cifar.html"> CIFAR-10 dataset</a>.</p>

![seagull]({{ site.baseurl }}/assets/640px-Mosaicr_seagull.jpg)

Image of a seagull comprising tiny hexagons. No, we're not recreating this, but something similar!

<p>A little backstory: last semester, I was the teaching assistant for <a href="http://pages.cs.wisc.edu/~dyer/cs534/">CS534 Computational Photography</a> here at Wisconsin, and at the end of the semester I was asked, by a commissioner who projected a silhouette of a bat onto the Wisconsin night sky, to come up with new assignment ideas. This idea of a photographic mosaicker didn't make the cut because it didn't fit in our existing syllabus, but the effect is so strong and the approach is so simple that I thought I'd share it here!</p>
<h2>You'll need</h2>
<ul>
    <li><strong>An input image.</strong> This is a fairly large color image that you want the mosaic to look like. Let the size of the image be <em>H×W</em><strong><strong><em>.</em></strong></strong>
    </li>
    <li><strong>A library of tiny images</strong>. We use a subset of the CIFAR-10 dataset. Let the number of tiny images be N<sub>t</sub>.</li>
    <li><strong>MATLAB with the statistics toolbox</strong>, or any language with a nearest neighbor implementation.</li>
</ul>
<h2>Steps</h2>
<ol>
    <li><strong>Shrink your tiny images to an appropriate size <em>D×D</em>.</strong> If <em>D</em> is large, you can recognize the content of the tiny images within the mosaic and that looks impressive, but the mosaic becomes coarse and starts looking less like the input image; if <em>D </em>is small, the mosaic reconstructs the input image well, but you can't tell what's in the tiny images, which kind of defeats the purpose of such a mosaic. You've got to strike a balance.</li>
    <li><strong>Shave off the borders of the input image</strong>, so that the height and width are each multiples of <em>D</em>, otherwise you can't create the mosaic effect at the 'leftover' portions of the input image.</li>
    <li><strong>Unroll the input image patches and the tiny images</strong>, into the observation matrix <em>X</em> and query matrix <em>Y</em>, respectively. X should be a N<sub>t</sub>×D<sup>2</sup> matrix since each D×D tiny image is unrolled into a vector of length D<sup>2</sup>. Similarly, you should cut up the H×W input image into many non-overlapping D×D patches, unrolled to produce a (HW⁄D<sup>2</sup>)×D<sup>2</sup> matrix.</li>
    <li><strong>Run 1-nearest-neighbors!</strong> Here we're just finding the most similar (in Euclidean distance between raw pixel intensities) tiny image for every patch in the input image.</li>
    <li><strong>Replace every patch in the input image with its nearest neighbor</strong> found in the previous step. Depending on your actual implementation, you probably have to roll the tiny images back into squares in this step.</li>
    <li><strong>And... we're done!</strong></li>
</ol>
<h2>Results</h2>
<p>Below we use a scene of Madison's beautiful Lake Mendota as the input image. You can't take such a picture now, not just because the lake is frozen now, but also because Memorial Union is closed off for renovations. But when it's accessible Lake Mendota is gorgeous. I digress.</p>

![sunset]({{ site.baseurl }}/assets/sunset.jpg)
Input image of Lake Mendota, WI Madison

![sunset mosaic]({{ site.baseurl }}/assets/sunset_mosaic.png)
Image mosaic of Lake Mendota comprising CIFAR-10 images

<p>The effect is really good for such a simple approach! Notice that we used raw pixel intensities to find nearest neighbors, which is probably a bad feature representation since we really don't care about the spatial distribution  of colors within the tiny image - we just need the colors between the input image patch and its tiny image to match. Something like a histogram of intensities along with Earthmover's distance would be more effective but complicates the code slightly. Here we overcame the limitation of using raw pixel intensities by shrinking the tiny images to be really tiny, so that we get a decent distribution of observations in feature space. The drawback, as mentioned, is that you can barely make out what the tiny images are within the mosaic.</p>
<p>Hope this was helpful!</p>
<p>(A gist of the above algorithm can be found <a href="https://gist.github.com/boonjiashen/a4d87b36f07c30a792c3">here</a>)</p>

