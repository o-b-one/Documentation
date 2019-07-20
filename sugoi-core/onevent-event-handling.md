---
description: Handling in-instance events with channel based
---

# @OnEvent - event handling

## Overview

SugoiJS provides a way to emit and handle events based on channels.

## Usage

### Listening to event

#### overview

Using the `@OnEvent` decorator we can bind the decorated method with the event.

`OnEvent(event: string, once?: boolean, channel?: string)  
  
event - Event name to bind to  
once - Should listen to the event once (default: false)  
channel - The channel name of the event tunnel (default: 'DEFAULT')`

#### Example

```typescript
import {OnEvent} from '@sugoi/server';

class EventHandler{
    CHANNEL_NAME: string = 'FIRST_CHANNEL';
    completed: boolean = false;
    
    @OnEvent('data', false, EventHandler.CHANNEL_NAME)    
    onData(data: any){
        if(this.completed){
            return;
        }
        // handle the emitted data
        processData(data);
    }
    
    @OnEvent('complete', true, EventHandler.CHANNEL_NAME)
    onComplete(){
        this.completed = true;
    }
    
}
```

### Emit event

#### overview

Using the @sugoi/server `EventEmitter` class we can emit data based on channels

`const emitter = new EventEmitter(channelName)  
  
channel - The channel name of the event tunnel (default: 'DEFAULT')`

#### 

#### Example

```typescript
const emitter = new EventEmitter('FIRST_CHANNEL');
emitter.emit('event', data)
```

### Full example

```typescript
import {OnEvent, EventEmitter} from '@sugoi/server';

class EventHandler{
    CHANNEL_NAME: string = 'FIRST_CHANNEL';
    completed: boolean = false;
    emitter: EventEmitter = new EventEmitter(EventHandler.CHANNEL_NAME);   
    
    @OnEvent('data', false, EventHandler.CHANNEL_NAME)    
    onData(data: any){
        if(this.completed){
            return;
        }
        // handle the emitted data
        processData(data);
    }
    
    @OnEvent('complete', true, EventHandler.CHANNEL_NAME)
    onComplete(){
        this.completed = true;
    }
    
    emit(event: string, ...data?: any){
        this.emitter.emit(event, ...data);
    }
    
}
```

