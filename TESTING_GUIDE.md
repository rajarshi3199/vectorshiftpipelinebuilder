# Testing Guide: Backend Integration

This guide will help you verify that the frontend-backend integration is working correctly.

## Prerequisites

1. **Python 3.8+** installed
2. **Node.js and npm** installed
3. Both frontend and backend folders accessible

## Step 1: Install Backend Dependencies

Open a terminal and navigate to the backend directory:

```bash
cd backend-20260115T180401Z-3-001/backend
pip install -r requirements.txt
```

Or install manually:
```bash
pip install fastapi uvicorn[standard] pydantic
```

## Step 2: Start the Backend Server

In the backend directory, run:

```bash
uvicorn main:app --reload
```

**Expected output:**
```
INFO:     Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)
INFO:     Started reloader process
INFO:     Started server process
INFO:     Waiting for application startup.
INFO:     Application startup complete.
```

✅ **Backend is running if you see this!**

### Test Backend Directly (Optional)

Open your browser and go to: `http://localhost:8000/`

You should see: `{"Ping":"Pong"}`

Or check the API docs at: `http://localhost:8000/docs`

## Step 3: Start the Frontend Server

Open a **NEW terminal window** and navigate to the frontend directory:

```bash
cd frontend-20260115T180021Z-3-001/frontend
npm install  # Only needed first time
npm start
```

**Expected output:**
```
Compiled successfully!

You can now view frontend in the browser.

  Local:            http://localhost:3000
```

✅ **Frontend is running if you see this!**

The browser should automatically open to `http://localhost:3000`

## Step 4: Test the Integration

### Test Case 1: Simple Pipeline (Should be DAG)

1. **Create a simple pipeline:**
   - Drag an **Input** node onto the canvas
   - Drag a **Text** node onto the canvas
   - Drag an **Output** node onto the canvas
   - Connect them: Input → Text → Output

2. **Click "Submit Pipeline" button**

3. **Expected Result:**
   - A modal alert should appear
   - Shows:
     - Number of Nodes: **3**
     - Number of Edges: **2**
     - Is DAG: **Yes** (green badge)

✅ **If you see this, integration is working!**

### Test Case 2: Pipeline with Cycle (Should NOT be DAG)

1. **Create a cycle:**
   - Drag 2 nodes (e.g., **Text** and **Transform**)
   - Connect: Text → Transform
   - Connect: Transform → Text (creates a cycle)

2. **Click "Submit Pipeline"**

3. **Expected Result:**
   - Modal shows:
     - Number of Nodes: **2**
     - Number of Edges: **2**
     - Is DAG: **No** (red badge)

✅ **If you see "Is DAG: No", cycle detection is working!**

### Test Case 3: Empty Pipeline

1. **Don't add any nodes**
2. **Click "Submit Pipeline"**

3. **Expected Result:**
   - Number of Nodes: **0**
   - Number of Edges: **0**
   - Is DAG: **Yes** (empty graph is a DAG)

### Test Case 4: Complex Pipeline

1. **Create a more complex pipeline:**
   - Input → Text → Filter → Output
   - Text → Transform → Output

2. **Click "Submit Pipeline"**

3. **Expected Result:**
   - Should show correct node/edge counts
   - DAG status depends on whether there are cycles

## Troubleshooting

### Problem: "Failed to connect to backend"

**Symptoms:**
- Error message in the alert modal
- Button shows "Submitting..." but never completes

**Solutions:**
1. ✅ Check if backend is running on port 8000
2. ✅ Verify backend shows "Uvicorn running on http://127.0.0.1:8000"
3. ✅ Check browser console (F12) for CORS errors
4. ✅ Make sure backend CORS allows `http://localhost:3000`

### Problem: Backend won't start

**Solutions:**
1. ✅ Check Python version: `python --version` (should be 3.8+)
2. ✅ Install dependencies: `pip install -r requirements.txt`
3. ✅ Check if port 8000 is already in use
4. ✅ Try: `uvicorn main:app --reload --port 8000`

### Problem: Frontend won't start

**Solutions:**
1. ✅ Run `npm install` first
2. ✅ Check Node.js version: `node --version`
3. ✅ Check if port 3000 is already in use
4. ✅ Clear cache: `npm cache clean --force`

### Problem: CORS errors in browser console

**Symptoms:**
- Browser console shows CORS policy errors

**Solutions:**
1. ✅ Verify backend `main.py` has CORS middleware configured
2. ✅ Check that `allow_origins` includes `http://localhost:3000`
3. ✅ Restart backend server after changes

## Quick Verification Checklist

- [ ] Backend server running on port 8000
- [ ] Frontend server running on port 3000
- [ ] Can access `http://localhost:8000/` and see `{"Ping":"Pong"}`
- [ ] Can create nodes and edges in frontend
- [ ] "Submit Pipeline" button works
- [ ] Alert modal appears with results
- [ ] DAG detection works correctly (test with and without cycles)

## Expected Behavior Summary

| Scenario | Nodes | Edges | Is DAG? |
|----------|-------|-------|---------|
| Empty canvas | 0 | 0 | Yes |
| Input → Output | 2 | 1 | Yes |
| Input → Text → Output | 3 | 2 | Yes |
| Text → Transform → Text (cycle) | 2 | 2 | No |
| Complex valid pipeline | N | N-1 | Yes |

## Success Indicators

✅ **Everything is working if:**
1. Backend starts without errors
2. Frontend loads in browser
3. You can drag nodes and create connections
4. Submit button shows loading state
5. Alert modal appears with correct data
6. DAG detection correctly identifies cycles

If all these work, your integration is successful! 🎉


