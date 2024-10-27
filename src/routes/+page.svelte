<script lang="ts">
  import { createClient } from '@supabase/supabase-js';

  const supabaseUrl = import.meta.env.VITE_SUPABASE_URL;
  const supabaseAnonKey = import.meta.env.VITE_SUPABASE_ANON_KEY;

  const supabase = createClient(supabaseUrl, supabaseAnonKey);

  let selectedFile: File | null = null;

  const uploadImage = async () => {
    if (selectedFile) {
      const { data, error } = await supabase.storage
        .from('images')
        .upload(`public/${selectedFile.name}`, selectedFile);

      if (error) {
        console.error('Error uploading image:', error);
      } else {
        console.log('Image uploaded:', data);
        // Call your API to generate alt text
      }
    }
  };
</script>

<input type="file" bind:this={selectedFile} />
<button class="btn btn-primary" on:click={uploadImage}>
  Upload and Generate Alt Text
</button>
