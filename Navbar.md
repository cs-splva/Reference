``` HTML
<!--
	HTML, CSS & JQuery Navbar for dashboards
	V1 19-3-2020
	Tested in Spotfire 10.6.1 app & webplayer
	David-van.Dorsten@klm.com
//-->

<!-- Navigation bar -->
<DIV class=page-header>

	<!-- Sidebar button -->
	<DIV>
		<img class="menu-button" onclick="activateSidebar('open');" src="https://cs-splva.github.io/images/menu.png"/>
	</DIV>

	<!-- Navigation bar -->
	<DIV class=page-title>
		<P><!-- Title of Dashboard --></P></DIV>
		<DIV class=page-menu>
		<UL>
		<LI class=active>
		<P><!-- Title of currently active page --></P></LI>
		<LI>
		<P><!-- Spotfire actionbutton navigate to page --></P></LI>
		<LI>
		<P><!-- Spotfire actionbutton navigate to page --></P></LI>
		</UL>
	</DIV>

	<!-- Fullscreen buttons, only work in Firefox & Chrome -->
	<button class="resize open" onclick="openFullscreen();">
	Fullscreen
	<img src="https://cs-splva.github.io/images/resize_big.png">
	</button>
	<button class="resize close" onclick="closeFullscreen();">
	Exit
	<img src="https://cs-splva.github.io/images/resize_small.png">
	</button>

	<!-- Right side logo's -->
	<div class=dit>
		<p>Data Integrity Team</p>
	</div>

	<DIV class=logo>
		<img class=klm-logo src="https://cs-splva.github.io/images/klm_logo.png" style="border: 0;"/>
	</DIV>

</DIV>
<!-- End Navigation bar -->

<!-- Sidebar -->
<DIV id="sidebar">
<p style="text-align:right;font-size:18px;">
<a onclick="activateSidebar('close');" style="cursor:pointer;">close ☒</a>
</p>

	<!-- accordion -->
	<DIV class=accordion>
		
		<H3>Item 1</H3>    
		<DIV>
			<P>
				Content
			</P>
		</DIV>

		<H3>Item 2</H3>
		<DIV>
			<P>
				Content
			</P>
		</DIV>
	</DIV>
	<!-- End Accordion -->

</DIV>
<!-- End Sidebar -->

<!-- Scripts & Stylesheet imports -->

<script src="https://cs-splva.github.io/js/navbar.js"></script>
<script src="https://cs-splva.github.io/js/accordion.js"></script>

<style>
@import url('https://cs-splva.github.io/css/style.css');

<!-- additional css could be placed here -->
</style>

```
