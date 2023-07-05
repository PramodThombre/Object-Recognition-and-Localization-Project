# Object-Recognition-and-Localization-Project
Finding top face of the watch from a point cloud data of a scanned wrist and watch

This file has 3 methods of finding a top face of the watch dial.

1. First align the clean_wrist mesh to the worn_wrist mesh so that all the cordinates will be in the reference of worn_wrist using ICP (Iterative Closest Point) function from trimesh library.
2. Using sklearn.neighbors LocalOutlierFactor to get the points outside the wrist which will be points of the watch.
3. Using PCA to get the major axis of the Outlier points. Get the radius, height and the transformation matrix using the minimum bounding cylinder to the aligned clean_wrist mesh. 
This way we know the span of the wrist and its radius.
4. Create a bounding box and use the transformation matrix to align them with the aligned clean wrist mesh. 
This way only the points of the dial are left out of the bounding boxes. (A cylindrical, sphere or a cubical bounding box can be used)
5. Now find the points that are outside the bounding box and the sphere.
6. Now this is like inverted plate shaped point cloud. Using PCA get the axis(surface normal) to the bottom of the inverted plate and project the points to this plane.
Compute convex hull of projected point cloud. Calculate the center by taking mean of the convex hull projected points.

<img width="480" alt="Screenshot 2023-07-05 at 2 23 57 AM" src="https://github.com/PramodThombre/Object-Recognition-and-Localization-Project/assets/61206092/2f7ec2b2-1ba5-4840-9c07-cfd3085831c8">

Scanned point data of hand with and without wrist watch.
<img width="521" alt="Screenshot 2023-07-05 at 2 24 40 AM" src="https://github.com/PramodThombre/Object-Recognition-and-Localization-Project/assets/61206092/e0376462-4fac-4b03-a166-ae028dcdf7cd">

Circular and cubic Bounding box created around the wrist watch.
<img width="410" alt="Screenshot 2023-07-05 at 2 25 00 AM" src="https://github.com/PramodThombre/Object-Recognition-and-Localization-Project/assets/61206092/baf62bba-d55f-45d6-ba64-dbda53656519">

Cylindrical bounding box created around the wrist watch.
