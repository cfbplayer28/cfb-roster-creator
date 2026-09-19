<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CFB 27 Roster Creator</title>
    <style>
        :root {
            --bg-main: #090d16;
            --bg-panel: #111827;
            --bg-input: #1f2937;
            --border-color: #374151;
            --accent-gold: #f59e0b;
            --accent-gold-hover: #d97706;
            --accent-blue: #3b82f6;
            --accent-blue-hover: #2563eb;
            --text-main: #f3f4f6;
            --text-muted: #9ca3af;
            --green: #34d399;
            --red: #f87171;
        }

        body { 
            font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; 
            background: var(--bg-main); 
            color: var(--text-main); 
            padding: 32px 24px; 
            max-width: 1280px; 
            margin: auto; 
        }

        header {
            margin-bottom: 24px;
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 16px;
            display: flex;
            justify-content: space-between;
            align-items: flex-end;
        }

        h1 { 
            color: var(--accent-gold); 
            text-transform: uppercase; 
            font-size: 24px;
            font-weight: 900; 
            letter-spacing: 1.5px; 
            margin: 0 0 4px 0; 
        }

        .controls-section {
            background: var(--bg-panel);
            padding: 20px;
            border-radius: 14px;
            margin-bottom: 24px;
            border: 1px solid var(--border-color);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.3);
            display: flex;
            flex-direction: column;
            gap: 16px;
        }

        .controls-row {
            display: flex;
            gap: 20px;
            align-items: center;
            flex-wrap: wrap;
        }

        .input-group {
            display: flex;
            flex-direction: column;
            gap: 6px;
            font-size: 12px;
            font-weight: 700;
            color: var(--text-muted);
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .input-group select, .input-group input {
            background: var(--bg-input);
            border: 1px solid var(--border-color);
            color: var(--text-main);
            font-family: monospace;
            font-size: 14px;
            padding: 9px 12px;
            border-radius: 8px;
            font-weight: 600;
            outline: none;
            transition: border-color 0.2s;
        }

        .input-group select:focus, .input-group input:focus {
            border-color: var(--accent-gold);
        }

        .input-group select {
            cursor: pointer;
            color: var(--accent-gold);
        }

        .dev-sliders-container {
            background: var(--bg-main);
            padding: 16px;
            border-radius: 10px;
            border: 1px solid var(--border-color);
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .dev-sliders-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 12px;
            font-weight: 700;
            text-transform: uppercase;
            color: var(--text-muted);
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 8px;
        }

        .dev-sliders-header span {
            color: var(--accent-gold);
            font-family: monospace;
        }

        .dev-sliders {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 14px;
        }

        .dev-slider-item {
            display: flex;
            flex-direction: column;
            gap: 4px;
            font-size: 12px;
            font-weight: 700;
            color: var(--text-muted);
        }

        .dev-slider-item input[type="range"] {
            cursor: pointer;
            accent-color: var(--accent-gold);
        }

        .dev-slider-val {
            color: var(--accent-gold);
            font-family: monospace;
        }

        .btn-container {
            display: flex;
            gap: 10px;
            align-items: center;
            margin-left: auto;
        }

        button { 
            background: var(--accent-gold); 
            color: var(--bg-main); 
            border: none; 
            padding: 11px 20px; 
            cursor: pointer; 
            border-radius: 8px; 
            font-weight: 800; 
            font-size: 13px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            transition: all 0.2s ease;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.2);
        }

        button:hover { 
            background: var(--accent-gold-hover); 
            transform: translateY(-1px);
        }

        button.alt { 
            background: var(--accent-blue); 
            color: white; 
        }
        
        button.alt:hover { 
            background: var(--accent-blue-hover); 
        }

        #status { 
            color: var(--text-muted); 
            font-size: 13px; 
            font-weight: 600; 
            background: var(--bg-input);
            padding: 8px 14px;
            border-radius: 8px;
            border: 1px solid var(--border-color);
        }

        .table-container { 
            background: var(--bg-panel); 
            border-radius: 14px; 
            border: 1px solid var(--border-color); 
            overflow-x: auto; 
            max-height: 620px;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.3);
        }

        table { 
            width: 100%; 
            border-collapse: collapse; 
            text-align: left; 
        }

        th, td { 
            padding: 14px 18px; 
            border-bottom: 1px solid var(--border-color); 
            font-size: 13px; 
        }

        th { 
            background: var(--bg-main); 
            color: var(--text-muted); 
            text-transform: uppercase; 
            font-size: 11px; 
            letter-spacing: 1px; 
            position: sticky; 
            top: 0; 
            z-index: 10;
        }

        tr:hover { 
            background: rgba(55, 65, 81, 0.3); 
        }

        .badge-dev {
            background: rgba(245, 158, 11, 0.1); 
            color: var(--accent-gold); 
            padding: 4px 10px; 
            border-radius: 6px; 
            font-size: 11px; 
            font-weight: 700;
            border: 1px solid rgba(245, 158, 11, 0.2);
            text-transform: uppercase;
        }

        .empty-state {
            text-align: center; 
            color: var(--text-muted); 
            padding: 60px 20px;
            font-size: 14px;
        }
    </style>
</head>
<body>

    <header>
        <div>
            <h1>CFB 27 Roster Creator</h1>
        </div>
    </header>
    
    <div class="controls-section">
        <div class="controls-row">
            <div class="input-group">
                <label for="tierSelect">Program Star Tier</label>
                <select id="tierSelect">
                    <option value="1star">1 Star</option>
                    <option value="2star" selected>2 Star</option>
                    <option value="3star">3 Star</option>
                    <option value="4star">4 Star</option>
                    <option value="5star">5 Star</option>
                    <option value="custom">Custom Sliders</option>
                </select>
            </div>

            <div class="input-group">
                <label for="offenseOvr">Offense OVR</label>
                <input type="number" id="offenseOvr" min="25" max="99" value="45">
            </div>

            <div class="input-group">
                <label for="defenseOvr">Defense OVR</label>
                <input type="number" id="defenseOvr" min="25" max="99" value="45">
            </div>

            <span id="status">Players generated: 0</span>

            <div class="btn-container">
                <button id="generateBtn">Generate Roster</button>
                <button id="exportBtn" class="alt">Export Studio CSV</button>
            </div>
        </div>

        <div class="dev-sliders-container">
            <div class="dev-sliders-header">
                <span>Dev Trait Distribution Weights</span>
                <span>Total Balance: <span id="totalSumVal">100</span>%</span>
            </div>
            <div class="dev-sliders">
                <div class="dev-slider-item">
                    <label>Normal Trait %: <span id="normalVal" class="dev-slider-val">65%</span></label>
                    <input type="range" id="sliderNormal" min="0" max="100" value="65" data-trait="normal">
                </div>
                <div class="dev-slider-item">
                    <label>Impact Trait %: <span id="impactVal" class="dev-slider-val">25%</span></label>
                    <input type="range" id="sliderImpact" min="0" max="100" value="25" data-trait="impact">
                </div>
                <div class="dev-slider-item">
                    <label>Star Trait %: <span id="starVal" class="dev-slider-val">8%</span></label>
                    <input type="range" id="sliderStar" min="0" max="100" value="8" data-trait="star">
                </div>
                <div class="dev-slider-item">
                    <label>Elite Trait %: <span id="eliteVal" class="dev-slider-val">2%</span></label>
                    <input type="range" id="sliderElite" min="0" max="100" value="2" data-trait="elite">
                </div>
            </div>
        </div>
    </div>

    <div class="table-container">
        <table id="rosterTable">
            <thead>
                <tr>
                    <th>Player Name</th>
                    <th>Pos</th>
                    <th>OVR</th>
                    <th>Class</th>
                    <th>Jersey</th>
                    <th>Weight</th>
                    <th>Height</th>
                    <th>Dev Trait</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td colspan="8" class="empty-state">Configure your targets and traits, then click <strong>"Generate Roster"</strong>.</td>
                </tr>
            </tbody>
        </table>
    </div>

<script>
let currentRoster = [];
const allPositions = ['QB', 'HB', 'WR', 'TE', 'LT', 'LG', 'C', 'RG', 'RT', 'LE', 'RE', 'DT', 'LOLB', 'MLB', 'ROLB', 'CB', 'FS', 'SS', 'K', 'P'];
const offensePositions = ['QB', 'HB', 'WR', 'TE', 'LT', 'LG', 'C', 'RG', 'RT', 'K', 'P'];

const baseFirstNames = [
    "PJ", "AJ", "TJ", "CJ",
    "Mark", "Paul", "Peter", "George", "Frank", "Carl", "Arthur", "Vincent", "Joel", "Patrick",
    "Sean", "Brett", "Cory", "Clint", "Dean", "Erik", "Lance", "Wade", "Seth", "Troy",
    "Zeke", "Titus", "Blaze", "Jaxson", "Kyson", "Zayden", "Kingston", "Krue", "Orion",
    "Jagger", "Zephyr", "Rocco", "Koa", "Boden", "Soren", "Thatcher", "Sterling", "Bridger", "Lawson",
    "Amari", "Cisero", "Kendal", "Truett", "Cyrus", "Dario", "Remi", "Penn", "Wells", "Sutton",
    "Leandro", "Idris", "Cassian", "Vance", "Kellan",
    "Damon", "Zane", "Rylan", "Axel", "Ryder", "Jude", "Kai", 
    "Knox", "Milo", "Kobe", "Atlas", "Rhett", "Dax", "Cruz", 
    "Ronin", "Kian", "Boone", "Kaison", "Kasen", "Colt", "Tyson", 
    "Brantley", "Remington", "Stetson", "Cash", "Ridge", "Huxley",
    "Blake", "Chase", "Cole", "Gavin", "Preston", "Spencer", "Tanner", "Wyatt", 
    "Cody", "Travis", "Derek", "Trevor", "Austin", "Logan", "Hunter", "Dakota", 
    "Dalton", "Garrett", "Brock", "Grant", "Jared", "Shane",
    "Liam", "Noah", "Oliver", "Theodore", "Henry", "Benjamin", "Levi", 
    "Elias", "Luca", "Jack", "Sebastian", "Hudson", "Leo", "Ezra", 
    "Daniel", "Ethan", "Julian", "Santiago", "Cooper", "Asher", "Owen", 
    "Luke", "Thomas", "Gabriel", "Mason", "Bennett", "Dylan", 
    "Roman", "Jacob", "Miles", "Carter", "Anthony", "Isaac", "Charles", 
    "Maverick", "Thiago",
    "Michael", "Alexander", "Matthew", "Steve", "Stephen", "Kyle", "Joseph", 
    "Brian", "Bryan", "Declan", "Samuel", "Nicholas", "Kevin", "Connor",
    "John", "David", "James", "Robert", "William", "Tyler", "Brandon", 
    "Zachary", "Justin", "Andrew", "Ryan", "Christian", "Nathan", "Aaron",
    "Jackson", "Trey", "Malik", "Cade", "Brayden", "Zion", "Xavier", "Colton", 
    "Dante", "Jaden", "Tyrell", "Brody", "Kaden", "Elijah", "Isaiah", "Damian", 
    "Keegan", "Jaxon", "Bryce", "Lucas", "Mateo", "Desmond", "Gage", "Kyler", 
    "Jalen", "Caelen", "Donovan", "Nash", "Deion"
];

const lastNames = [
    "Vaughn", "Sutton", "Landry", "Chambers", "Bowers", "Potter", "Vance", "Dixon",
    "Schultz", "Bauer", "Bishop", "McCarthy", "Flynn", "Cunningham", "Lane",
    "Knight", "Melton", "Odom", "Parrish", "Stark", "Conner", "Abbott", "Atkinson",
    "Benton", "Brady", "Carey", "Coffey", "Duffy", "Eaton", "Gentry", "Glover",
    "Harding", "Holder", "Kemp", "Lang", "Mann", "McClain", "McIntyre", "Nixon",
    "Phelps", "Rigney", "Sampson", "Sellers", "Tate", "Wade", "Yates",
    "Zimmerman", "Davenport",
    "Toney", "Webster", "Webber", "Banks", "Fletcher", "George", 
    "Jensen", "Wagner", "Lofton", "Blanton", "Harper", "Rose", 
    "Fulton", "Lyon", "Dean", "Bain", "Waters", "Steed", "Wilcox", "Platt", "Hopkins",
    "Garcia", "Martinez", "Hernandez", "Lopez", "Gonzalez", 
    "Patterson", "Washington", "Simmons", "Griffin", "Freeman", "Hill", "Hilton",
    "Hart", "Coleman", "Conley", "Hayes", "Myers", "Ford", "Hamilton", "Graham", 
    "Sullivan", "Wallace", "Woods", "Cole", "West", "Jordan", "Owens", "Reynolds", 
    "Fisher", "Ellis", "Harrison", "Gibson", "McDonald", "Marshall", "Murray",
    "Smith", "Johnson", "Williams", "Brown", "Jones", "Miller", "Davis", "Wilson",
    "Anderson", "Taylor", "Thomas", "Moore", "Jackson", "Martin", "Lee", "Perez",
    "Thompson", "White", "Harris", "Sanchez", "Clark", "Ramirez", "Lewis", "Robinson",
    "Walker", "Young", "Allen", "King", "Wright", "Scott", "Torres", "Nguyen",
    "Flores", "Green", "Adams", "Nelson", "Baker", "Hall", "Rivera",
    "Campbell", "Mitchell", "Carter", "Roberts", "Phillips", "Evans", "Turner",
    "Diaz", "Parker", "Cruz", "Edwards", "Collins", "Reyes", "Stewart", "Morris",
    "Morales", "Murphy", "Cook", "Rogers", "Gutierrez", "Ortiz", "Morgan", "Cooper",
    "Peterson", "Bailey", "Reed", "Kelly", "Howard", "Ramos", "Kim", "Cox",
    "Ward", "Richardson", "Watson", "Brooks", "Chavez", "Wood", "James", "Bennett",
    "Gray", "Mendoza", "Ruiz", "Hughes", "Price", "Alvarez", "Castillo", "Sanders",
    "Patel", "Long", "Ross", "Foster", "Jimenez", "Powell", "Jenkins",
    "Perry", "Russell", "Bell", "Butler", "Henderson", "Barnes", "Berger", "Meeks", "Weeks"
];

const homeTowns = [
    { town: 'Birmingham', state: 0 }, { town: 'Montgomery', state: 0 }, { town: 'Mobile', state: 0 }, { town: 'Tuscaloosa', state: 0 }, { town: 'Huntsville', state: 0 }, { town: 'Auburn', state: 0 },
    { town: 'Anchorage', state: 1 }, { town: 'Fairbanks', state: 1 }, { town: 'Juneau', state: 1 }, { town: 'Wasilla', state: 1 },
    { town: 'Phoenix', state: 2 }, { town: 'Tucson', state: 2 }, { town: 'Scottsdale', state: 2 }, { town: 'Mesa', state: 2 }, { town: 'Flagstaff', state: 2 }, { town: 'Tempe', state: 2 },
    { town: 'Little Rock', state: 3 }, { town: 'Fayetteville', state: 3 }, { town: 'Fort Smith', state: 3 }, { town: 'Conway', state: 3 }, { town: 'Bentonville', state: 3 },
    { town: 'Los Angeles', state: 4 }, { town: 'San Diego', state: 4 }, { town: 'San Francisco', state: 4 }, { town: 'Sacramento', state: 4 }, { town: 'Fresno', state: 4 }, { town: 'Oakland', state: 4 },
    { town: 'Denver', state: 5 }, { town: 'Colorado Springs', state: 5 }, { town: 'Boulder', state: 5 }, { town: 'Fort Collins', state: 5 }, { town: 'Pueblo', state: 5 },
    { town: 'Hartford', state: 6 }, { town: 'New Haven', state: 6 }, { town: 'Stamford', state: 6 }, { town: 'Storrs', state: 6 }, { town: 'Bridgeport', state: 6 },
    { town: 'Wilmington', state: 7 }, { town: 'Dover', state: 7 }, { town: 'Newark', state: 7 }, { town: 'Middletown', state: 7 },
    { town: 'Miami', state: 8 }, { town: 'Orlando', state: 8 }, { town: 'Tampa', state: 8 }, { town: 'Jacksonville', state: 8 }, { town: 'Tallahassee', state: 8 }, { town: 'St. Augustine', state: 8 }, { town: 'Gainesville', state: 8 },
    { town: 'Atlanta', state: 9 }, { town: 'Savannah', state: 9 }, { town: 'Augusta', state: 9 }, { town: 'Athens', state: 9 }, { town: 'Marietta', state: 9 }, { town: 'Valdosta', state: 9 },
    { town: 'Honolulu', state: 10 }, { town: 'Hilo', state: 10 }, { town: 'Kailua', state: 10 }, { town: 'Pearl City', state: 10 },
    { town: 'Boise', state: 11 }, { town: 'Idaho Falls', state: 11 }, { town: 'Pocatello', state: 11 }, { town: 'Coeur d’Alene', state: 11 },
    { town: 'Chicago', state: 12 }, { town: 'Springfield', state: 12 }, { town: 'Peoria', state: 12 }, { town: 'Champaign', state: 12 }, { town: 'Rockford', state: 12 }, { town: 'Evanston', state: 12 },
    { town: 'Indianapolis', state: 13 }, { town: 'Bloomington', state: 13 }, { town: 'West Lafayette', state: 13 }, { town: 'South Bend', state: 13 }, { town: 'Fort Wayne', state: 13 },
    { town: 'Des Moines', state: 14 }, { town: 'Iowa City', state: 14 }, { town: 'Ames', state: 14 }, { town: 'Cedar Rapids', state: 14 }, { town: 'Davenport', state: 14 },
    { town: 'Wichita', state: 15 }, { town: 'Overland Park', state: 15 }, { town: 'Kansas City', state: 15 }, { town: 'Lawrence', state: 15 }, { town: 'Manhattan', state: 15 },
    { town: 'Louisville', state: 16 }, { town: 'Lexington', state: 16 }, { town: 'Bowling Green', state: 16 }, { town: 'Frankfort', state: 16 }, { town: 'Owensboro', state: 16 },
    { town: 'New Orleans', state: 17 }, { town: 'Baton Rouge', state: 17 }, { town: 'Shreveport', state: 17 }, { town: 'Lafayette', state: 17 }, { town: 'Ruston', state: 17 },
    { town: 'Portland', state: 18 }, { town: 'Bangor', state: 18 }, { town: 'Lewiston', state: 18 }, { town: 'Augusta', state: 18 }, { town: 'Orono', state: 18 },
    { town: 'Baltimore', state: 19 }, { town: 'Annapolis', state: 19 }, { town: 'Silver Spring', state: 19 }, { town: 'Frederick', state: 19 }, { town: 'College Park', state: 19 },
    { town: 'Boston', state: 20 }, { town: 'Worcester', state: 20 }, { town: 'Springfield', state: 20 }, { town: 'Cambridge', state: 20 }, { town: 'Amherst', state: 20 },
    { town: 'Detroit', state: 21 }, { town: 'Grand Rapids', state: 21 }, { town: 'Ann Arbor', state: 21 }, { town: 'Lansing', state: 21 }, { town: 'Kalamazoo', state: 21 }, { town: 'Traverse City', state: 21 },
    { town: 'Minneapolis', state: 22 }, { town: 'St. Paul', state: 22 }, { town: 'Duluth', state: 22 }, { town: 'Rochester', state: 22 }, { town: 'Bloomington', state: 22 },
    { town: 'Jackson', state: 23 }, { town: 'Gulfport', state: 23 }, { town: 'Hattiesburg', state: 23 }, { town: 'Oxford', state: 23 }, { town: 'Starkville', state: 23 },
    { town: 'St. Louis', state: 24 }, { town: 'Kansas City', state: 24 }, { town: 'Springfield', state: 24 }, { town: 'Columbia', state: 24 }, { town: 'Independence', state: 24 },
    { town: 'Billings', state: 25 }, { town: 'Missoula', state: 25 }, { town: 'Bozeman', state: 25 }, { town: 'Helena', state: 25 },
    { town: 'Omaha', state: 26 }, { town: 'Lincoln', state: 26 }, { town: 'Bellevue', state: 26 }, { town: 'Grand Island', state: 26 },
    { town: 'Las Vegas', state: 27 }, { town: 'Reno', state: 27 }, { town: 'Henderson', state: 27 }, { town: 'Carson City', state: 27 },
    { town: 'Manchester', state: 28 }, { town: 'Nashua', state: 28 }, { town: 'Concord', state: 28 }, { town: 'Durham', state: 28 },
    { town: 'Newark', state: 29 }, { town: 'Jersey City', state: 29 }, { town: 'Trenton', state: 29 }, { town: 'Princeton', state: 29 }, { town: 'Atlantic City', state: 29 },
    { town: 'Albuquerque', state: 30 }, { town: 'Santa Fe', state: 30 }, { town: 'Las Cruces', state: 30 }, { town: 'Roswell', state: 30 },
    { town: 'New York City', state: 31 }, { town: 'Buffalo', state: 31 }, { town: 'Syracuse', state: 31 }, { town: 'Albany', state: 31 }, { town: 'Rochester', state: 31 }, { town: 'Ithaca', state: 31 },
    { town: 'Charlotte', state: 32 }, { town: 'Raleigh', state: 32 }, { town: 'Greensboro', state: 32 }, { town: 'Durham', state: 32 }, { town: 'Asheville', state: 32 }, { town: 'Boone', state: 32 },
    { town: 'Fargo', state: 33 }, { town: 'Bismarck', state: 33 }, { town: 'Grand Forks', state: 33 }, { town: 'Minot', state: 33 },
    { town: 'Columbus', state: 34 }, { town: 'Cleveland', state: 34 }, { town: 'Cincinnati', state: 34 }, { town: 'Canton', state: 34 }, { town: 'Dayton', state: 34 }, { town: 'Massillon', state: 34 },
    { town: 'Oklahoma City', state: 35 }, { town: 'Tulsa', state: 35 }, { town: 'Norman', state: 35 }, { town: 'Stillwater', state: 35 }, { town: 'Edmond', state: 35 },
    { town: 'Portland', state: 36 }, { town: 'Eugene', state: 36 }, { town: 'Salem', state: 36 }, { town: 'Corvallis', state: 36 }, { town: 'Bend', state: 36 },
    { town: 'Philadelphia', state: 37 }, { town: 'Pittsburgh', state: 37 }, { town: 'Harrisburg', state: 37 }, { town: 'Lancaster', state: 37 }, { town: 'York', state: 37 }, { town: 'State College', state: 37 }, { town: 'Allentown', state: 37 },
    { town: 'Providence', state: 38 }, { town: 'Newport', state: 38 }, { town: 'Warwick', state: 38 }, { town: 'Cranston', state: 38 },
    { town: 'Columbia', state: 39 }, { town: 'Charleston', state: 39 }, { town: 'Greenville', state: 39 }, { town: 'Spartanburg', state: 39 }, { town: 'Clemson', state: 39 }, { town: 'Myrtle Beach', state: 39 },
    { town: 'Sioux Falls', state: 40 }, { town: 'Rapid City', state: 40 }, { town: 'Aberdeen', state: 40 }, { town: 'Brookings', state: 40 },
    { town: 'Nashville', state: 41 }, { town: 'Memphis', state: 41 }, { town: 'Knoxville', state: 41 }, { town: 'Chattanooga', state: 41 }, { town: 'Murfreesboro', state: 41 }, { town: 'Bristol', state: 41 },
    { town: 'Dallas', state: 42 }, { town: 'Houston', state: 42 }, { town: 'Austin', state: 42 }, { town: 'San Antonio', state: 42 }, { town: 'Katy', state: 42 }, { town: 'Lubbock', state: 42 }, { town: 'College Station', state: 42 }, { town: 'Southlake', state: 42 },
    { town: 'Salt Lake City', state: 43 }, { town: 'Provo', state: 43 }, { town: 'Logan', state: 43 }, { town: 'Ogden', state: 43 }, { town: 'Park City', state: 43 },
    { town: 'Burlington', state: 44 }, { town: 'Montpelier', state: 44 }, { town: 'Rutland', state: 44 }, { town: 'Stowe', state: 44 },
    { town: 'Richmond', state: 45 }, { town: 'Virginia Beach', state: 45 }, { town: 'Norfolk', state: 45 }, { town: 'Roanoke', state: 45 }, { town: 'Blacksburg', state: 45 }, { town: 'Charlottesville', state: 45 },
    { town: 'Seattle', state: 46 }, { town: 'Spokane', state: 46 }, { town: 'Tacoma', state: 46 }, { town: 'Vancouver', state: 46 }, { town: 'Pullman', state: 46 }, { town: 'Olympia', state: 46 },
    { town: 'Charleston', state: 47 }, { town: 'Morgantown', state: 47 }, { town: 'Huntington', state: 47 }, { town: 'Parkersburg', state: 47 },
    { town: 'Milwaukee', state: 48 }, { town: 'Madison', state: 48 }, { town: 'Green Bay', state: 48 }, { town: 'Kenosha', state: 48 }, { town: 'Eau Claire', state: 48 },
    { town: 'Cheyenne', state: 49 }, { town: 'Casper', state: 49 }, { town: 'Laramie', state: 49 }, { town: 'Jackson', state: 49 }
];

let activeSliderChanging = false;

document.addEventListener("DOMContentLoaded", () => {
    document.getElementById("generateBtn").addEventListener("click", generateRoster);
    document.getElementById("exportBtn").addEventListener("click", exportStudioCSV);
    
    const tierSelect = document.getElementById("tierSelect");
    const offInput = document.getElementById("offenseOvr");
    const defInput = document.getElementById("defenseOvr");
    
    const sNorm = document.getElementById("sliderNormal");
    const sImp = document.getElementById("sliderImpact");
    const sStar = document.getElementById("sliderStar");
    const sElite = document.getElementById("sliderElite");

    const sliders = [sNorm, sImp, sStar, sElite];

    function updateLabelsAndTotal() {
        document.getElementById("normalVal").innerText = sNorm.value + '%';
        document.getElementById("impactVal").innerText = sImp.value + '%';
        document.getElementById("starVal").innerText = sStar.value + '%';
        document.getElementById("eliteVal").innerText = sElite.value + '%';

        const sum = parseInt(sNorm.value) + parseInt(sImp.value) + parseInt(sStar.value) + parseInt(sElite.value);
        document.getElementById("totalSumVal").innerText = sum;
    }

    sliders.forEach(slider => {
        slider.addEventListener("input", (e) => {
            if (activeSliderChanging) return;
            activeSliderChanging = true;
            tierSelect.value = "custom";

            const changedSlider = e.target;
            const targetVal = parseInt(changedSlider.value);
            
            const otherSliders = sliders.filter(s => s !== changedSlider);
            let currentOtherSum = otherSliders.reduce((acc, s) => acc + parseInt(s.value), 0);
            
            let desiredOtherSum = 100 - targetVal;
            if (desiredOtherSum < 0) desiredOtherSum = 0;

            if (currentOtherSum === 0) {
                let split = Math.floor(desiredOtherSum / otherSliders.length);
                otherSliders.forEach(s => s.value = split);
                otherSliders[0].value = parseInt(otherSliders[0].value) + (desiredOtherSum - (split * otherSliders.length));
            } else {
                let allocated = 0;
                for (let i = 0; i < otherSliders.length; i++) {
                    let s = otherSliders[i];
                    if (i === otherSliders.length - 1) {
                        s.value = Math.max(0, Math.min(100, desiredOtherSum - allocated));
                    } else {
                        let proportion = parseInt(s.value) / currentOtherSum;
                        let newVal = Math.round(desiredOtherSum * proportion);
                        s.value = Math.max(0, Math.min(100, newVal));
                        allocated += parseInt(s.value);
                    }
                }
            }

            updateLabelsAndTotal();
            activeSliderChanging = false;
        });
    });

    tierSelect.addEventListener("change", (e) => {
        const val = e.target.value;
        activeSliderChanging = true;
        if (val === '1star') {
            offInput.value = 28; defInput.value = 28;
            sNorm.value = 85; sImp.value = 12; sStar.value = 3; sElite.value = 0;
        } else if (val === '2star') {
            offInput.value = 45; defInput.value = 45;
            sNorm.value = 65; sImp.value = 25; sStar.value = 8; sElite.value = 2;
        } else if (val === '3star') {
            offInput.value = 72; defInput.value = 72;
            sNorm.value = 40; sImp.value = 35; sStar.value = 20; sElite.value = 5;
        } else if (val === '4star') {
            offInput.value = 86; defInput.value = 86;
            sNorm.value = 20; sImp.value = 30; sStar.value = 35; sElite.value = 15;
        } else if (val === '5star') {
            offInput.value = 95; defInput.value = 95;
            sNorm.value = 5; sImp.value = 15; sStar.value = 40; sElite.value = 40;
        }
        updateLabelsAndTotal();
        activeSliderChanging = false;
    });
});

function generateRoster() {
    currentRoster = [];
    const tier = document.getElementById("tierSelect").value;
    const targetOffense = parseInt(document.getElementById("offenseOvr").value) || 45;
    const targetDefense = parseInt(document.getElementById("defenseOvr").value) || 45;
    
    let availableFirstNames = [...baseFirstNames];
    const usedFullNames = new Set();
    
    const mandatoryPositions = [
        'QB', 'QB', 'QB',
        'HB', 'HB', 'HB', 'HB', 
        'WR', 'WR', 'WR', 'WR', 'WR', 'WR', 'WR',
        'TE', 'TE', 'TE',
        'LT', 'LT', 'LG', 'LG', 'C', 'C', 'RG', 'RG', 'RT', 'RT',
        'DT', 'DT', 'DT', 'DT',
        'LE', 'LE', 'RE', 'RE', 
        'LOLB', 'LOLB', 'MLB', 'MLB', 'MLB', 'ROLB', 'ROLB',
        'CB', 'CB', 'CB', 'CB', 'CB',
        'FS', 'FS', 'SS', 'SS',
        'K', 'P'
    ];
    
    mandatoryPositions.forEach((pos, index) => {
        const isOffense = offensePositions.includes(pos);
        const target = isOffense ? targetOffense : targetDefense;
        currentRoster.push(createPlayer(pos, index + 1, target, tier, availableFirstNames, usedFullNames));
    });

    for (let i = currentRoster.length + 1; i <= 85; i++) {
        const pos = allPositions[Math.floor(Math.random() * allPositions.length)];
        const isOffense = offensePositions.includes(pos);
        const target = isOffense ? targetOffense : targetDefense;
        currentRoster.push(createPlayer(pos, i, target, tier, availableFirstNames, usedFullNames));
    }
    
    currentRoster.sort((a, b) => b.overall - a.overall);
    renderTable();
    document.getElementById('status').innerText = `Players generated: ${currentRoster.length}`;
}

function getPositionHeightAndWeight(pos) {
    switch(pos) {
        case 'LT': case 'LG': case 'C': case 'RG': case 'RT':
            return { height: Math.floor(Math.random() * 4) + 75, weight: Math.floor(Math.random() * 45) + 285 };
        case 'DT':
            return { height: Math.floor(Math.random() * 4) + 73, weight: Math.floor(Math.random() * 40) + 275 };
        case 'TE': case 'LE': case 'RE': case 'LOLB': case 'MLB': case 'ROLB':
            return { height: Math.floor(Math.random() * 5) + 73, weight: Math.floor(Math.random() * 35) + 235 };
        case 'QB': case 'FS': case 'SS': case 'P': case 'K':
            return { height: Math.floor(Math.random() * 5) + 71, weight: Math.floor(Math.random() * 30) + 195 };
        case 'HB':
            return { height: Math.floor(Math.random() * 5) + 68, weight: Math.floor(Math.random() * 30) + 190 };
        case 'WR': case 'CB':
            return { height: Math.floor(Math.random() * 5) + 70, weight: Math.floor(Math.random() * 25) + 175 };
        default:
            return { height: 73, weight: 210 };
    }
}

function getDevTraitCode() {
    const pNorm = parseInt(document.getElementById("sliderNormal").value) || 0;
    const pImp = parseInt(document.getElementById("sliderImpact").value) || 0;
    const pStar = parseInt(document.getElementById("sliderStar").value) || 0;
    const pElite = parseInt(document.getElementById("sliderElite").value) || 0;
    
    let total = pNorm + pImp + pStar + pElite;
    if (total <= 0) total = 100;

    const roll = Math.random() * total;
    
    if (roll < pNorm) return { name: 'Normal', code: 0 };
    if (roll < pNorm + pImp) return { name: 'Impact', code: 1 };
    if (roll < pNorm + pImp + pStar) return { name: 'Star', code: 2 };
    return { name: 'Elite', code: 3 };
}

function createPlayer(pos, jerseyNum, targetOvr, tier, availableFirstNames, usedFullNames) {
    let fName, lName, fullName;
    let safetyCounter = 0;
    
    do {
        if (availableFirstNames.length === 0) {
            availableFirstNames.push(...baseFirstNames);
        }
        
        const fIndex = Math.floor(Math.random() * availableFirstNames.length);
        fName = availableFirstNames[fIndex];
        
        lName = lastNames[Math.floor(Math.random() * lastNames.length)];
        fullName = `${fName} ${lName}`;
        safetyCounter++;
    } while (usedFullNames.has(fullName) && safetyCounter < 100);
    
    const nameIndex = availableFirstNames.indexOf(fName);
    if (nameIndex > -1) {
        availableFirstNames.splice(nameIndex, 1);
    }
    
    usedFullNames.add(fullName);

    let variance = tier === '1star' ? 3 : 5;
    let ovr = targetOvr + Math.floor(Math.random() * (variance * 2 + 1)) - variance;
    ovr = Math.min(99, Math.max(20, ovr));

    let hw = getPositionHeightAndWeight(pos);
    let townObj = homeTowns[Math.floor(Math.random() * homeTowns.length)];
    let dev = getDevTraitCode();

    // Lock primary archetype stats directly to the target OVR so Team Builder's formula evaluates the exact rating
    return {
        firstName: fName,
        lastName: lName,
        position: pos,
        jerseyNumber: jerseyNum <= 99 ? jerseyNum : Math.floor(Math.random() * 90) + 1,
        classYear: ['FR', 'SO', 'JR', 'SR'][Math.floor(Math.random() * 4)],
        heightInches: hw.height,
        weightLbs: hw.weight,
        isLefty: "FALSE",
        skinTone: Math.floor(Math.random() * 7),
        portraitId: "",
        devTrait: dev.code,
        devTraitName: dev.name,
        homeTown: townObj.town,
        homeTownState: townObj.state,
        overall: ovr,
        // Position-weighted attribute mapping matching the CSV schema
        SPD: ['HB', 'WR', 'CB', 'FS', 'SS', 'LOLB', 'ROLB'].includes(pos) ? ovr : randAttr(ovr), 
        STR: ['LT', 'LG', 'C', 'RG', 'RT', 'DT', 'LE', 'RE'].includes(pos) ? ovr : randAttr(ovr), 
        AGI: ['HB', 'WR', 'QB'].includes(pos) ? ovr : randAttr(ovr), 
        ACC: ['HB', 'WR', 'CB'].includes(pos) ? ovr : randAttr(ovr), 
        AWR: ovr, 
        BTK: pos === 'HB' ? ovr : randAttr(ovr), 
        TRK: randAttr(ovr), 
        COD: randAttr(ovr), 
        BCV: pos === 'HB' ? ovr : randAttr(ovr), 
        SFA: randAttr(ovr),
        SPM: randAttr(ovr), 
        JKM: randAttr(ovr), 
        CAR: pos === 'HB' ? ovr : randAttr(ovr), 
        CTH: ['WR', 'TE'].includes(pos) ? ovr : randAttr(ovr), 
        SRR: ['WR', 'TE'].includes(pos) ? ovr : randAttr(ovr), 
        MRR: ['WR', 'TE'].includes(pos) ? ovr : randAttr(ovr), 
        DRR: pos === 'WR' ? ovr : randAttr(ovr), 
        CIT: ['WR', 'TE'].includes(pos) ? ovr : randAttr(ovr), 
        SPC: randAttr(ovr), 
        RLS: randAttr(ovr),
        JMP: randAttr(ovr), 
        THP: pos === 'QB' ? ovr : randAttr(ovr), 
        SAC: pos === 'QB' ? ovr : randAttr(ovr), 
        MAC: pos === 'QB' ? ovr : randAttr(ovr), 
        DAC: pos === 'QB' ? ovr : randAttr(ovr), 
        RUN: randAttr(ovr), 
        TUP: pos === 'QB' ? ovr : randAttr(ovr), 
        BSK: pos === 'QB' ? ovr : randAttr(ovr), 
        PAC: randAttr(ovr), 
        TAK: ['MLB', 'LOLB', 'ROLB', 'CB', 'FS', 'SS', 'DT', 'DE'].includes(pos) ? ovr : randAttr(ovr),
        POW: randAttr(ovr), 
        PMV: ['LE', 'RE', 'DT'].includes(pos) ? ovr : randAttr(ovr), 
        FMV: ['LE', 'RE', 'DT'].includes(pos) ? ovr : randAttr(ovr), 
        BSH: ['LE', 'RE', 'DT', 'MLB'].includes(pos) ? ovr : randAttr(ovr), 
        PUR: randAttr(ovr), 
        PRC: ovr, 
        MCV: randAttr(ovr), 
        ZCV: ['CB', 'FS', 'SS'].includes(pos) ? ovr : randAttr(ovr), 
        PRS: randAttr(ovr), 
        PBK: ['LT', 'LG', 'C', 'RG', 'RT'].includes(pos) ? ovr : randAttr(ovr),
        PBP: ['LT', 'LG', 'C', 'RG', 'RT'].includes(pos) ? ovr : randAttr(ovr), 
        PBF: ['LT', 'LG', 'C', 'RG', 'RT'].includes(pos) ? ovr : randAttr(ovr), 
        RBK: ['LT', 'LG', 'C', 'RG', 'RT', 'TE'].includes(pos) ? ovr : randAttr(ovr), 
        RBP: randAttr(ovr), 
        RPF: randAttr(ovr),
        LBK: randAttr(ovr), 
        IBL: randAttr(ovr), 
        KPW: pos.match(/[KP]/) ? ovr : randAttr(ovr), 
        KAC: pos.match(/[KP]/) ? ovr : randAttr(ovr), 
        RET: randAttr(ovr),
        STA: 85, INJ: 90, TGH: 85, LSP: 5
    };
}

function randAttr(ovr) {
    // Ultra-tight variance to prevent Team Builder's formula from recalculating a different OVR
    return Math.min(99, Math.max(20, ovr + Math.floor(Math.random() * 5) - 2));
}

function renderTable() {
    const tbody = document.querySelector('#rosterTable tbody');
    tbody.innerHTML = '';
    
    currentRoster.forEach(p => {
        let ovrColor = p.overall >= 80 ? 'color: var(--green); font-weight: 800;' : p.overall >= 65 ? 'color: var(--text-main); font-weight: 700;' : 'color: var(--red); font-weight: 800;';
        let ft = Math.floor(p.heightInches / 12);
        let inch = p.heightInches % 12;
        tbody.innerHTML += `<tr>
            <td style="font-weight: 600;">${p.firstName} ${p.lastName}</td>
            <td style="font-family: monospace; color: var(--accent-gold); font-weight: 800;">${p.position}</td>
            <td style="${ovrColor}">${p.overall}</td>
            <td style="color: var(--text-muted); font-family: monospace; font-weight: 600;">${p.classYear}</td>
            <td style="color: var(--text-muted); font-family: monospace; font-weight: 600;">#${p.jerseyNumber}</td>
            <td style="color: var(--text-muted); font-family: monospace; font-weight: 600;">${p.weightLbs} lbs</td>
            <td style="color: var(--text-muted); font-family: monospace; font-weight: 600;">${ft}'${inch}"</td>
            <td><span class="badge-dev">${p.devTraitName}</span></td>
        </tr>`;
    });
}

function exportStudioCSV() {
    if (currentRoster.length === 0) {
        alert("Please generate a roster first before exporting!");
        return;
    }

    const headers = [
        "firstName", "lastName", "position", "jerseyNumber", "classYear", "heightInches", "weightLbs", "isLefty", "skinTone", "portraitId", "devTrait", "homeTown", "homeTownState",
        "SPD", "STR", "AGI", "ACC", "AWR", "BTK", "TRK", "COD", "BCV", "SFA", "SPM", "JKM", "CAR", "CTH", 
        "SRR", "MRR", "DRR", "CIT", "SPC", "RLS", "JMP", "THP", "SAC", "MAC", "DAC", "RUN", "TUP", "BSK", 
        "PAC", "TAK", "POW", "PMV", "FMV", "BSH", "PUR", "PRC", "MCV", "ZCV", "PRS", "PBK", "PBP", "PBF", 
        "RBK", "RBP", "RPF", "LBK", "IBL", "KPW", "KAC", "RET", "STA", "INJ", "TGH", "LSP"
    ];

    let csvContent = headers.join(",") + "\n";

    currentRoster.forEach(p => {
        let row = headers.map(h => {
            let val = p[h] !== undefined ? p[h] : 50;
            return typeof val === 'string' ? `"${val}"` : val;
        });
        csvContent += row.join(",") + "\n";
    });

    const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
    const url = URL.createObjectURL(blob);
    const dlAnchor = document.createElement('a');
    dlAnchor.setAttribute("href", url);
    dlAnchor.setAttribute("download", "cfb27_teambuilder_roster.csv");
    document.body.appendChild(dlAnchor);
    dlAnchor.click();
    dlAnchor.remove();
}
</script>

</body>
</html>
