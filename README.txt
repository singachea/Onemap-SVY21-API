// By Ream Lim, [singachea(at)gmail.com]
// Version: 1.0
// Date: January, 2012


This is a simple (perhaps minimal for getting the coordinates and addresses) api to call onemap sg written in C# . I do this because I couldn't find available library in C#, and it was annoying to deal with weird Singapore coordinates system (SVY21) from onemap. The below is what you can do with this simple library:

 * Convert back and forth between Singapore Geo System (SYV21: X, Y / Easting, Northing) and Google Map (WGS84: Longitude, Latitude)
 * Retrieve the onemap token from a key
 * Retrieve coordinates from onemap from search key
 * Retrieve address from onemap from search key

HOW TO USE THIS LIBRARY
-----------------------
	1. Add both .dll files (Utils.dll and Systems.Web.Extension.dll) into your project reference
	2. Use it :P


EXAMPLE
-------
	
	using System;
	using System.Collections.Generic;
	using System.Linq;
	using System.Text;

	using ReamSGOneMap.Utils;

	namespace ReamSGOneMap
	{
		class Program
		{
			static void Main(string[] args)
			{
				Console.WriteLine("----------------------- CONVERT (X,Y) VS (LONGITUDE, LATITUDE) -----------------------");

				GeoCoordinates geoXY = new GeoCoordinates(29535.0995308659, 28912.1833258747, false);
				Console.WriteLine("Longitude: {0}, Latitude: {1}", geoXY.Longitude, geoXY.Latitude);

				GeoCoordinates geoLL = new GeoCoordinates(103.847112019776, 1.2777459830532, true);
				Console.WriteLine("X: {0}, Y: {1}", geoLL.X, geoLL.Y);

				Console.WriteLine();
				Console.WriteLine("----------------------- GET TOKEN FROM A KEY -----------------------");

				string key = "qo/s2TnSUmfLz+32CvLC4RMVkzEFYjxqyti1KhByvEacEdMWBpCuSSQ+IFRT84QjGPBCuz/cBom8PfSm3GjEsGc8PkdEEOEr";
				var token = OneMapToken.GetTokenFromAccessKey(key);
				Console.WriteLine("Key: {0} --> Token: {1}", key, token);

				Console.WriteLine();
				Console.WriteLine("----------------------- GET COORDINATES FROM SEARCH KEY -----------------------");

				string samplePostalCode = "081004";
				var coordinates = OneMapHelper.GetCooridnates(token, samplePostalCode);
				Console.WriteLine("Longitude: {0}, Latitude: {1}", coordinates.Longitude, coordinates.Latitude);
				Console.WriteLine("X: {0}, Y: {1}", coordinates.X, coordinates.Y);

				Console.WriteLine();
				Console.WriteLine("----------------------- GET GEO-ADDRESS FROM SEARCH KEY -----------------------");

				var geoAddress = OneMapHelper.GetGeoAddress(token, samplePostalCode);
				Console.WriteLine("HBRN: {0}, Building name: {1}, Postal code: {2}", geoAddress.HBRN, geoAddress.BLDG_NAME, geoAddress.PostalCode);
				Console.WriteLine(geoAddress.GetAddressString());

				Console.WriteLine();
				Console.WriteLine("----------------------- USING INSTANCE STYLE -----------------------");
				// you can also use object
				var geoObject = new OneMapHelper(token);
				var coor = geoObject.GetCooridnates(samplePostalCode);
				Console.WriteLine("Longitude: {0}, Latitude: {1}", coor.Longitude, coor.Latitude);

				var addr = geoObject.GetGeoAddress(samplePostalCode);
				Console.WriteLine(addr.GetAddressString());
				
			}
		}
	}
	
	
	
Oh yeah, I also have Google Map api written in C# as well. If you want it contact me [singachea(at)gmail.com]
