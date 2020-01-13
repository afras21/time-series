# Fetching data based on (Month, Week, Today)

Instead of fetching all the data and displaying we are fetching date based on the above 3 criteria.

**Setting up date values**

    // Getting date and time
    currentDate = new Date();
    const now = Date.now();
    const oneDay = (1000 * 60 * 60 * 24);
    const today = new Date(now - (now % oneDay));
    const tomorrow = new Date(today.valueOf() + oneDay);
    const monthStartDay = new Date(currentDate.getFullYear(), currentDate.getMonth(), 1);
    const weekStartDay =  new  Date(currentDate.setDate(currentDate.getDate() - currentDate.getDay()));
    
**Fetching a Month's transactions**

    // merge with the userQuery containing user parameters(attributes)
    
    monthQuery = _.merge({}, userQuery, { 
	    'metadata.createdAt': {
		 $gte: monthStartDay.toISOString(),
		 $lt: tomorrow.toISOString()
		   }
		 });
**Fetching a Weekly transactions**

    // merge with the userQuery containing user parameters(attributes)
    
    weekQuery = _.merge({}, userQuery, { 
	    'metadata.createdAt': {
		 $gte: weekStartDay.toISOString(),
		 $lt: tomorrow.toISOString()
		   }
		 });
**Fetching a Daily transactions**

    // merge with the userQuery containing user parameters(attributes)
    
    weekQuery = _.merge({}, userQuery, { 
	    'metadata.createdAt': {
		 $gte: today.toISOString(),
		 $lt: tomorrow.toISOString()
		   }
		 });
