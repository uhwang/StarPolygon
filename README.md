# StarPolygon
12/23/2023

How To Draw Star Polygons?

Definition of Star Polygons

- Star polygons are inscribed in a circle of given radius.

- Star polygons have outer vertices and inner vertices.

- To find the inner vertices of a star polygon, we need to calculate the intersection points of the lines formed by the outer vertices. However, the calculation is different for the case where there are 3 or 4 outer vertices.

**1. Define Star Polygon**

<img src="images/image1.png" style="width:3.28125in;height:3.59375in" />

**2. Calculate outer vertices**

n : the number of outer vertices

<img src="images/media/image2.png" style="width:3.73958in;height:1.22917in" /><img src="images/media/image3.png" style="width:2.21875in;height:2.15625in" />

**3. Calculate Inner Vertices**

- <img src="images/media/image4.png" style="width:2.91667in;height:2.53125in" />**Case 1: n=3 or 4**

<img src="images/media/image5.png" style="width:4.22917in;height:3.25in" />

- **Case 2: n \> 4**

> Find the intersection point of two lines of given four outer vertices. The slopes of two lines are normal.

<img src="images/media/image6.png" style="width:3.88542in;height:3.86458in" /><img src="images/media/image7.png" style="width:4.65625in;height:4.3125in" />

- **When x1=x2 or x3=x4**

<img src="images/media/image8.png" style="width:4.125in;height:2.25in" />

**4. Intersection Point Line Index Sequence**

<table style="width:100%;">
<colgroup>
<col style="width: 20%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 22%" />
</colgroup>
<thead>
<tr class="header">
<th>i</th>
<th>0</th>
<th>1</th>
<th>2</th>
<th>3</th>
<th>4</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td rowspan="2"><p>First Line</p>
<p>Vertex Index</p></td>
<td>0</td>
<td>1</td>
<td>2</td>
<td>3</td>
<td>4</td>
<td><strong>i</strong></td>
</tr>
<tr class="even">
<td>2</td>
<td>3</td>
<td>4</td>
<td>0</td>
<td>1</td>
<td><strong>(i+2)%n</strong></td>
</tr>
<tr class="odd">
<td rowspan="2">Second Line Vertex Index</td>
<td>1</td>
<td>2</td>
<td>3</td>
<td>4</td>
<td>0</td>
<td><strong>(i+1)%n</strong></td>
</tr>
<tr class="even">
<td>4</td>
<td>0</td>
<td>1</td>
<td>2</td>
<td>3</td>
<td><strong>(n-1+i)%n</strong></td>
</tr>
</tbody>
</table>

**5. Star Polygon (n= 3, 4, 5, 6, 7, 8 )**

<img src="images/media/image9.png" style="width:5.83333in;height:4.30208in" alt="A group of images of a star Description automatically generated with medium confidence" />

**6. Move Inner Vertices**

<img src="images/media/image10.png" style="width:3.69792in;height:3.61458in" /><img src="images/media/image11.png" style="width:6.1875in;height:1.64583in" />

7\. Put All Together

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><p>import numpy as np</p>
<p>import matplotlib.pyplot as plt</p>
<p>def star_polygon(xc, yc, nvert, radius):</p>
<p>    vs = np.zeros(nvert*2*2+2)</p>
<p>    for k in range(nvert):</p>
<p>        angle = 0.5*(4*k+nvert)*np.pi/nvert</p>
<p>        vs[k*4] = xc+radius*np.cos(angle)</p>
<p>        vs[k*4+1] = yc+radius*np.sin(angle)</p>
<p>    vs[-1] = vs[1]</p>
<p>    vs[-2] = vs[0]</p>
<p>    xx = vs[0::4]</p>
<p>    yy = vs[1::4]</p>
<p>    if nvert == 3 or nvert == 4:</p>
<p>        default_u = nvert*0.1</p>
<p>        for i in range(nvert):</p>
<p>            angle = 2*np.pi*(i+1)/nvert+0.5*(nvert-2)*np.pi/nvert</p>
<p>            px = xc+default_u*radius*np.cos(angle)</p>
<p>            py = yc+default_u*radius*np.sin(angle)</p>
<p>            vs[2+i*4] = px</p>
<p>            vs[2+i*4+1] = py</p>
<p>    else:</p>
<p>        for i in range(nvert):</p>
<p>            i1 = i</p>
<p>            i2 = (i+2)%nvert</p>
<p>            i3 = (i+1)%nvert</p>
<p>            i4 = (nvert-1+i)%nvert</p>
<p>            x1, y1 = xx[i1], yy[i1]</p>
<p>            x2, y2 = xx[i2], yy[i2]</p>
<p>            x3, y3 = xx[i3], yy[i3]</p>
<p>            x4, y4 = xx[i4], yy[i4]</p>
<p>            if abs(x2-x1) &lt; 1e-10:</p>
<p>                m = (y4-y3)/(x4-x3)</p>
<p>                px= x1</p>
<p>                py= m*(px-x3)+y3</p>
<p>            elif abs(x3-x4) &lt; 1e-10:</p>
<p>                m = (y2-y1)/(x2-x1)</p>
<p>                px= x3</p>
<p>                py= m*(px-x1)+y1</p>
<p>            else:</p>
<p>                m1 = (y2-y1)/(x2-x1)</p>
<p>                m2 = (y4-y3)/(x4-x3)</p>
<p>                px = (m1*x1-y1-m2*x3+y3)/(m1-m2)</p>
<p>                py = m1*(px-x1)+y1</p>
<p>            vs[2+i*4] = px</p>
<p>            vs[2+i*4+1] = py</p>
<p>    return vs</p>
<p>def plot_star_polygon(subnum, vss):</p>
<p>    ax = plt.subplot(subnum)</p>
<p>    ax.plot(vss[0::2], vss[1::2])</p>
<p>    ax.scatter(vss[2::4], vss[3::4], color='hotpink')</p>
<p>    ax.scatter(vss[::4], vss[1::4], color='green')</p>
<p>    ax.axis('equal')</p>
<p>class StarPolygon:</p>
<p>    def __init__(self,</p>
<p>                 sx,</p>
<p>                 sy,</p>
<p>                 nvert=5,</p>
<p>                 radius  = 1,</p>
<p>        ) -&gt; None:</p>
<p>        if nvert &lt; 3:</p>
<p>            raise ValueError('nvert must be greater than equal 3')</p>
<p>        self.nvert = nvert</p>
<p>        self.sx = sx</p>
<p>        self.sy = sy</p>
<p>        self.vertex = star_polygon(sx, sy, nvert, radius)</p>
<p>        self._u_vertex = np.zeros(nvert*2)</p>
<p>        self._u_vertex[::2] = self.vertex[2::4]</p>
<p>        self._u_vertex[1::2] = self.vertex[3::4]</p>
<p>    def reset_uvertex(self):</p>
<p>        self.vertex[2::4] = self._u_vertex[0::2]</p>
<p>        self.vertex[3::4] = self._u_vertex[1::2]</p>
<p>    @property</p>
<p>    def xss(self):</p>
<p>        return self.vertex[0::2]</p>
<p>       </p>
<p>    @property</p>
<p>    def yss(self):</p>
<p>        return self.vertex[1::2]</p>
<p>    @property</p>
<p>    def pxs(self):</p>
<p>        return self.vertex[0::4]</p>
<p>    @property</p>
<p>    def pys(self):</p>
<p>        return self.vertex[1::4]</p>
<p>       </p>
<p>    @property</p>
<p>    def uxs(self):</p>
<p>        return self.vertex[3::4]</p>
<p>    @property</p>
<p>    def uys(self):</p>
<p>        return self.vertex[4::4]</p>
<p>       </p>
<p>    @property</p>
<p>    def u_radius(self):</p>
<p>        return np.sqrt(self.vertex[2]**2+self.vertex[3]**2)</p>
<p>       </p>
<p>    @property</p>
<p>    def u_param(self):</p>
<p>        return self._param_u</p>
<p>       </p>
<p>    # u -&gt; 1 : inner radius</p>
<p>    # u &lt; 1, u =1, u &gt; 1</p>
<p>    @u_param.setter</p>
<p>    def u_param(self, u):</p>
<p>        for i in range(self.nvert):</p>
<p>            self.vertex[2+i*4] = self.sx+(self._u_vertex[i*2]-self.sx)*u</p>
<p>            self.vertex[2+i*4+1] = self.sy+(self._u_vertex[i*2+1]-self.sy)*u</p>
<p>def move_uvertex(subnum, star):</p>
<p>    uu = np.linspace(0.5, 1.5, 4)</p>
<p>    for u in uu:</p>
<p>        star.u_param = u</p>
<p>        plt.subplot(subnum)</p>
<p>        plt.plot(star.xss, star.yss, color="k", linewidth=1)</p>
<p>def plot_all():</p>
<p>    stars = [StarPolygon(0,0,n) for n in range(3,9)]</p>
<p>    nrow, ncol = 2, 3</p>
<p>   </p>
<p>    for i, st in enumerate(stars):</p>
<p>        subnum = nrow*100+ncol*10+(i+1)</p>
<p>        move_uvertex(subnum, st)</p>
<p>        st.reset_uvertex()</p>
<p>        plot_star_polygon(subnum, st.vertex)</p>
<p>       </p>
<p>    plt.show()</p>
<p>plot_all()</p></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

<img src="images/media/image9.png" style="width:5.83333in;height:4.30208in" alt="A group of images of a star Description automatically generated with medium confidence" /><img src="images/media/image12.png" style="width:5.83333in;height:4.30208in" alt="A group of images of a star Description automatically generated with medium confidence" />

