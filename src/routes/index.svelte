<script lang="ts">
import Tabs from "$lib/Tabs.svelte";
import TabItem from "$lib/TabItem.svelte";
import Checkbox from "$lib/Checkbox.svelte";
import Container from "$lib/Container.svelte";

  let items = ['one', 'two', 'three'];
  let activeTab = 0;
</script>

<Container>
  <Tabs {items} bind:activeTab>
    <TabItem {activeTab} index={0}>
      <Container>
        One <Checkbox checked={true}>My CheckBox</Checkbox>
      </Container>
    </TabItem>
    <TabItem {activeTab} index={1}>
      <Container>
        Two
      </Container>
    </TabItem>
    <TabItem {activeTab} index={2}>
      <Container>
        Three
      </Container>
    </TabItem>
  </Tabs>
</Container>