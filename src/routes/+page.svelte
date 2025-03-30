<center >
<br>
    <h1 class="heading">Show Finder</h1>
<br>
<p style="font-size:20px">Let's find something to watch!</p>
</center>
<br>

<div class="cardContainer">
    <div class="cardColumn">
        <div class="card">
            <div class="card-body">How Much Time Do You Have?</div>
            <select class="select select-xs" bind:value={timeAnswer}>
                <option>Select 1</option>
                <option value="30min">⏳ 30 min Quick Episode</option>
                <option value="60-120">🕒 An Hour or Two</option>
                <option value="binge">🌙 I'm Binging All Night!</option>
            </select>
        </div>
        <div class="card">
            <div class="card-body">Animation or Live Action?</div>
            <select class="select select-xs" bind:value={animationAnswer}>
                <option value="">Select 1</option>
                <option value="yes">🎨 Animated Magic!</option>
                <option value="no">🧍🏾‍♀️ Human Faces, Real Places</option>
            </select>
        </div>
        <div class="card">
            <div class="card-body">Audience?</div>
            <select class="select select-xs" bind:value={audienceAnswer}>
                <option value="">Select 1</option>
                <option value="adults">🍷 Adults Only, Please</option>
                <option value="kids">🧸 Just For the Kids</option>
                <option value="family">🍿 Family Night</option>
            </select>
        </div>
    </div>
    <div class="cardColumn">
        <div class="card">
            <div class="card-body">What Are You In the Mood For?</div>
            <select class="select select-xs" bind:value={moodAnswer}>
                <option value="">Step 1</option>
                <option value="comedy">😂 Comedy</option>
                <option value="horror">😱 Horror</option>
                <option value="sci-fi">🚀 Sci-Fi</option>
                <option value="romance">🥰 Romance</option>
                <option value="fantasy">⚔️ Fantasy</option>
                <option value="mystery">🕵🏾 Mystery</option>
                <option value="musical">🎶 Musical</option> 
                <option value="super">🧙 Supernatural</option> 
                <option value="crime">👮‍♂️ Crime/Thriller</option> 
                            
            </select>
        </div>
        <div class="card">
            <div class="card-body">🌈 Looking for LGBTQ+ representation?</div>
            <select class="select select-xs" bind:value={lgbtAnswer}>
                <option value="">Select 1</option>
                <option value="yes">💖 Yes, please!</option>
                <option value="open">🤷 I'm open to it</option>
                <option value="no">🙅 No, not this time</option>
            </select>
        </div>
        <div class="card">
            <div class="card-body" >Pick a Setting You Like</div>
            <select class="select select-xs" bind:value={settingAnswer}>
                <option value="">Select 1</option>
                <option value="space">🚀 Space</option>
                <option value="high">🏫 High School</option>
                <option value="fantasy">🏰 Medieval/Fantasy</option>
                <option value="small">🏡 Small Town Drama</option>
                <option value="city">🏙️ Big City Chaos</option>
                <option value="future">🌌 Future/Dystopia</option>
                <option value="myth">🔮 Mythical or Supernatural</option> 
                <option value="historical">🏛️ 🏛️  Historical</option> 
                          


            </select>
        </div>
    </div>

</div>
<br><br>
<center><p ><button class="btn btn-outline-primary" on:click={getShow}>🎬 Find My Show!</button></p></center>
<br>
<center><p style="font-size:28px;color:blue">{message}</p></center>

<style>
    .heading{
        border-radius: 20px;
        border-style: solid;
        font-size: 24px;
        border-width: .5px;
        max-width: 50%;
        padding:8px;
        box-shadow: 10px 10px 5px inset blue;
    }

    .cardContainer{
        display: flex;         
        gap: 10px;             
        justify-content: center;
    }
       
    .cardColumn{
        display: flex;
        flex-direction: column; /* Stack boxes vertically */
        gap: 20px;
        
    }
     
    .card{
        border-radius: 8px;
        text-align: center;
        align-items: center;
        width: 400px;
        border-style: solid;
        border-color:blue;
        border-width: 1px;
        box-shadow: inset 0 4px 8px rgba(0, 123, 255, 0.4), inset 0 -2px 6px rgba(192, 192, 192, 0.3);

    }
        

    .flex.w-full.justify-center.gap-4{
        display: flex;
        /* flex-direction: row; */
    
    } 
  
</style>

<script>
    import {createClient} from '@supabase/supabase-js';
    const supabaseUrl = 'https://ggwbvoxyjczfbhsiyuaz.supabase.co';
    const supabaseKey = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Imdnd2J2b3h5amN6ZmJoc2l5dWF6Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3NDA5MjQyODAsImV4cCI6MjA1NjUwMDI4MH0.VhkEhjj9iBQux-hyeg44562tZrFHAKE-tHLQy4w5Koo';
    const supabase = createClient(supabaseUrl, supabaseKey);

    let timeAnswer;
    let animationAnswer;
    let audienceAnswer;
    let moodAnswer;
    let lgbtAnswer;
    let settingAnswer;
    let message;
    

    let matchingShows;
    async function getShow() 
    {
        let query = supabase
        .from("shows")
	    .select("*")
	    if (timeAnswer) query= query.eq("time", timeAnswer)
        if (animationAnswer)query.eq("animation", animationAnswer)
        if(audienceAnswer)query.eq("audience", audienceAnswer)
        if(moodAnswer)query.eq("genre", moodAnswer)
        if(lgbtAnswer)query = query.ilike("lgbt", `%${lgbtAnswer}%`)
        if(settingAnswer)query.eq("setting", settingAnswer)
        .limit(5)
        const { data, error } = await query

        if(data.length>0){
            showName= data[0].show_name
        }else{message="No Matching Shows"}
    }
    


    

</script>