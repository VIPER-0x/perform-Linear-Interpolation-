# perform-Linear-Interpolation-
ALGORITHM FOR perform Linear Interpolation 

// Function to perform Linear Interpolation  
function linearInterpolate(A, B, t):  
    // A and B are points (x, y)  
    // t is a normalized parameter (0 <= t <= 1) that defines the position between A and B  
    x_new = A.x + t * (B.x - A.x)  
    y_new = A.y + t * (B.y - A.y)  
    return (x_new, y_new)  

// Function to apply Extended Median Filter  
function extendedMedianWithInterpolation(dataPoints):  
    filteredPoints = []  // Array to hold filtered points  
    n = length(dataPoints)  
    
    // Step through data points to compute median and interpolate between points  
    for i from 0 to n-1:  
        // Get current data point  
        currentPoint = dataPoints[i]  
        
        // Create a list for storing surrounding points  
        surroundingPoints = []  
        
        // Collect surrounding points for median filtering  
        if i > 0:  
            surroundingPoints.append(dataPoints[i-1])  // Previous point  
        surroundingPoints.append(currentPoint)         // Current point  
        if i < n-1:  
            surroundingPoints.append(dataPoints[i+1])  // Next point  
        
        // Apply Median Filter on surrounding points  
        filteredPoint = medianFilter(surroundingPoints)  
        filteredPoints.append(filteredPoint)  

        // If there are points before and after, perform interpolation  
        if i > 0 and i < n-1:  
            // Interpolate between previous and next points  
            A = dataPoints[i-1]  
            C = dataPoints[i+1]  
            t = 0.5  // Midpoint interpolation  
            interPolatedPoint = linearInterpolate(A, C, t)  
            // Use interPolatedPoint as necessary for smoothing  
            filteredPoints[i] = interPolatedPoint  // Update filtered point with interpolated value  

    return filteredPoints  

// Main processing loop  
inputData = [(x1, y1), (x2, y2), (x3, y3), ...]  // Your (x, y) data points  
stabilizedData = extendedMedianWithInterpolation(inputData)  
// Use stabilizedData in your control system logic here
