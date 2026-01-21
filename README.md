<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    
    <title>VFD Pro</title>
    <link rel="manifest" href="manifest.json">
    <meta name="theme-color" content="#050505">
    
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="VFD Pro">
    <link rel="apple-touch-icon" href="icon.png">

    <style>
        /* ... Keep all your existing CSS here ... */
        @import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap');
        * { box-sizing: border-box; touch-action: manipulation; }
        
        body, html { 
            background-color: #050505; 
            height: 100vh; 
            width: 100vw; 
            margin: 0; 
            font-family: 'Share Tech Mono', monospace; 
            overflow: hidden; 
            position: fixed; 
        }

        .display-area { 
            background: #010808; 
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 45vh; 
            padding: 15px; 
            display: flex; 
            flex-direction: column; 
            z-index: 10;
        }

        .display-area::after { content: ""; position: absolute; top: 0; left: 0; width: 100%; height: 100%; background-image: radial-gradient(circle, transparent 20%, rgba(0,0,0,0.7) 70%); background-size: 2px 2px; pointer-events: none; z-index: 20; }
        
        .history-viewport { flex-grow: 1; overflow-y: auto; display: flex; flex-direction: column; scroll-behavior: smooth; }
        #history-container { margin-top: auto; display: flex; flex-direction: column; }
        
        .history-item { 
            display: flex; 
            flex-direction: column; 
            align-items: stretch; 
            justify-content: center; 
            min-height: 55px; 
            padding: 5px 15px; 
            margin: 2px 0; 
            font-size: 1.2rem; 
            color: #26bf9e; 
            opacity: 1; 
            flex-shrink: 0; 
        }
        
        .history-item span:first-child { align-self: flex-start; text-align: left; }
        .history-item span:last-child { align-self: flex-end; text-align: right; font-weight: bold; color: #33ffcc; }

        .history-item.selected { color: #000 !important; background: #33ffcc; opacity: 1; box-shadow: 0 0 15px rgba(51, 255, 204, 0.6); border-radius: 4px; }
        .history-item.selected span:first-child { color: #aaffee !important; }
        .history-item.selected span:last-child { color: #fff !important; text-shadow:
