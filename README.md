#Documentation

CONSTRUCTOR

new(name: string, scope: string, key: string)
"Returns previously created datastore session else a new session"

new(name: string, key: string)
"Returns previously created datastore session else a new session"

hidden(name: string, scope: string, key: string)
"Returns a new session that cannot be returned by new or find"

hidden(name: string, key: string)
"Returns a new session that cannot be returned by new or find"

find(name: string, scope: string, key: string)
"Returns previously created datastore session else nil"

find(name: string, key: string)
"Returns previously created datastore session else nil"

Response Success Saved Locked State Error
"List of responses that acts like a enum"

PROPERTIES

Value  any  nil
"Value of datastore"

Metadata  table  {}
"Metadata associated with the key"

UserIds  table  {}
"An array of UserIds associated with the key"

SaveInterval  number  30
"Interval in seconds the datastore will automatically save (set to 0 to disable automatic saving)"

SaveDelay  number  0
"Delay between saves"

LockInterval  number  60
"Interval in seconds the memorystore will update the session lock"

LockAttempts  number  5
"How many times the memorystore needs to fail before the session closes"

SaveOnClose  boolean  true
"Automatically save the data when the session is closed or destroyed"

Id  string  "Name/Scope/Key"  READ ONLY
"Identifying string"

UniqueId  string  "8-4-4-4-12"  READ ONLY
"Unique identifying string"
Key  string  "Key"  READ ONLY
"Key used for the datastore"

State  boolean?  false  READ ONLY
"Current state of the session [nil = Destroyed] [false = Closed] [true = Open]"

Hidden  boolean  false/true  READ ONLY
"Set to true if this session was created by the hidden constructor"

AttemptsRemaining  number  0  READ ONLY
"How many memorystore attempts remaining before the session closes"

CreatedTime  number  0  READ ONLY
"Number of milliseconds from epoch to when the datastore was created"

UpdatedTime  number  0  READ ONLY
"Number of milliseconds from epoch to when the datastore was updated (not updated while session is open)"

Version  string  ""  READ ONLY
"Unique identifying string of the current datastore save"

CompressedValue  string  ""  READ ONLY
"Compressed string that is updated before every save if compression is enabled by setting dataStore.Metadata.Compress = {["Level"] = 2, ["Decimals"] = 3, ["Safety"] = true}
Level = 1 (allows mixed tables), Level = 2 (does not allow mixed tables but compresses arrays better), Decimals = amount of decimal places saved, Safety = replace delete character from strings"

EVENTS

StateChanged(state: boolean?, dataStore: DataStore)  Signal
"Fires when the State property has changed"

Saving(value: any, dataStore: DataStore)  Signal
"Fires just before the value is about to save"

Saved(response: string, responseData: any, dataStore: DataStore)  Signal
"Fires after a save attempt"

AttemptsChanged(attemptsRemaining: number, dataStore: DataStore)  Signal
"Fires when the AttemptsRemaining property has changed"

ProcessQueue(id: string, values: array, dataStore: DataStore)  Signal
"Fires when state = true and values detected inside the MemoryStoreQueue"

METHODS

Open(template: any)  string any
"Tries to open the session, optional template parameter will be reconciled onto the value"

Read(template: any)  string any
"Reads the datastore value without the need to open the session, optional template parameter will be reconciled onto the value"

Save()  string any
"Force save the current value to the datastore"

Close()  string any
"Closes the session"

Destroy()  string any
"Closes and destroys the session, destroyed sessions will be locked"

Queue(value: any, expiration: number?, priority: number?)  string any
"Adds a value to the MemoryStoreQueue expiration default (604800 seconds / 7 days), max (3888000 seconds / 45 days)"

Remove(id: string)  string any
"Remove values from the MemoryStoreQueue"

Clone()  any
"Clones the value property"

Reconcile(template: any) nil
"Fills in missing values from the template into the value property"

Usage()  number number
"How much datastore has been used, returns the character count and the second number is a number scaled from 0 to 1 [0 = 0% , 0.5 = 50%, 1 = 100%, 1.5 = 150%]"
