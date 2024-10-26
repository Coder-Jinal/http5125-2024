# Back-End Web Development 1
Course Code: HTTP 5125

Academic Year: 2025-2026

In this course, students are introduced to server-side web development with the C# programming language, and will implement techniques for creating data-driven websites drawing from various external data sources.


# Links
https://www.geeksforgeeks.org/backend-development/

# Images

![Mymi pics](Backend-Development-ezgif.com-webp-to-jpg-converter.jpg).

> **Note**:This repository focuses on server-side functionality using C#. For those new to back-end development, it’s recommended to have a foundational understanding of databases and APIs, as these concepts are essential for creating dynamic, data-driven applications.

# Code Example:
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Routing.Template;

namespace Assignment2.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class J2 : Controller
    {
        /// <summary>
        /// It calculates overall spiciness of the chilli after adding the peppers
        /// </summary>
        /// <param name="items">The list of pepper names</param>
        /// <returns>It will return a number as the total spiciness</returns>
        /// <example>
        /// GET: "https://localhost:7049/api/J2/ChiliPeppers&Ingredients=Poblano,Cayenne,Thai,Poblano" --> 118000
        /// GET: "https://localhost:7049/api/J2/ChiliPeppers&Ingredients=Habanero,Habanero,Habanero,Habanero,Habanero" --> 625000
        /// GET: "https://localhost:7049/api/J2/ChiliPeppers&Ingredients=Poblano,Mirasol,Serrano,Cayenne,Thai,Habanero,Serrano" --> 278500
        /// </example>
        [HttpGet(template: "ChiliPeppers&Ingredients={items}")]
        public int spiciness(string items)
        {
            string[] Chillipeppers = items.Split(',');

            int totalspiciness = 0;

            foreach (var totalpepper in Chillipeppers)
            {
                switch (totalpepper.Trim())
                {
                    case "Poblano":
                        totalspiciness += 1500;
                        break;
                    case "Mirasol":
                        totalspiciness += 6000;
                        break;
                    case "Serrano":
                        totalspiciness += 15500;
                        break;
                    case "Cayenne":
                        totalspiciness += 40000;
                        break;
                    case "Thai":
                        totalspiciness += 75000;
                        break;
                    case "Habanero":
                        totalspiciness += 125000;
                        break;
                    default:
                        break;
                }
            }
            return totalspiciness;
        }


        /// <summary>
        /// Link: https://cemc.uwaterloo.ca/sites/default/files/documents/2021/2021CCCJrProblemSet.html
        /// A charity is having a silent auction where people place bids on a prize without knowing anyone else’s bid. Each bid includes a person’s name and the 
        /// amount of their bid. After the silent auction is over, the winner is the person who has placed the highest bid. If there is a tie, the person whose 
        /// bid was placed first wins. Your job is to determine the winner of the silent auction.
        /// </summary>
        /// <param name="N">Total number of bids</param>
        /// <param name="name">An array of list of people who has bid</param>
        /// <param name="bid">An array of list of bid amount</param>
        /// <returns>It will return the person who has the highest bid</returns>
        /// <example>
        /// GET: "https://localhost:7049/api/J2/silentbid?N=3&name=Ahmed&name=Suzanne&name=Ivona&bid=300&bid=500&bid=450" --> Suzanne
        /// GET:  "https://localhost:7049/api/J2/silentbid?N=2&name=Ijeoma&name=Goor&bid=20&bid=20" --> Ijeoma
        /// </example>
        [HttpGet(template:"silentbid")]
        public IActionResult silentbid ([FromQuery] int N, [FromQuery] string[] name, [FromQuery] int[] bid) 
        {

            string bidwinner = "";
            int biggestbid = -1;
            for (int i = 0; i < N; i++)
            {
                string namelist = name[i];
                int bidlist = bid[i];
                if (bidlist > biggestbid)
                {
                    biggestbid = bidlist;
                    bidwinner = namelist;
                }
            }

            return Ok(bidwinner);
           
        }
    }
}
